# git.ts - Git 集成

## 功能概述

`git.ts` 提供 Git 仓库操作的高级封装，包括：
- 查找 Git 根目录
- 解析 worktree 和 canonical root
- 获取 Git 状态（分支、commit、remote 等）
- stash 和 Git 状态保存

## 核心函数

### findGitRoot(startPath: string): string | null
通过向上遍历目录树查找 Git 根目录。

```typescript
export const findGitRoot = createFindGitRoot()
```

**逻辑：**
1. 从起始路径向上遍历
2. 查找 `.git` 目录（常规仓库）或 `.git` 文件（worktree/submodule）
3. 使用 LRU 缓存（最多 50 个条目）

**返回：**
- 包含 `.git` 的目录路径
- 如果未找到返回 `null`

### findCanonicalGitRoot(startPath: string): string | null
获取规范化的 Git 仓库根目录。

```typescript
export const findCanonicalGitRoot = createFindCanonicalGitRoot()
```

**与 findGitRoot 的区别：**
- 对于 worktree，返回主仓库的工作目录
- 解析 `.git` 文件中的 `gitdir:` 引用
- 通过 `commondir` 找到主仓库

**安全验证：**
1. 验证 `commondir` 结构匹配 `git worktree add` 创建的格式
2. 验证 worktree gitdir 指向主仓库的 `.git`

### getGitState(): Promise<GitRepoState | null>
获取完整的 Git 状态。

```typescript
export async function getGitState(): Promise<GitRepoState | null>
```

**返回：**
```typescript
type GitRepoState = {
  commitHash: string           // 当前 commit SHA
  branchName: string           // 分支名
  remoteUrl: string | null      // 远程 URL
  isHeadOnRemote: boolean      // HEAD 是否在远程
  isClean: boolean             // 工作区是否干净
  worktreeCount: number        // worktree 数量
}
```

### getFileStatus(): Promise<GitFileStatus>
获取文件状态（已跟踪 vs 未跟踪）。

```typescript
export const getFileStatus = async (): Promise<GitFileStatus>
```

**返回：**
```typescript
type GitFileStatus = {
  tracked: string[]     // 已跟踪的文件
  untracked: string[]   // 未跟踪的文件
}
```

### stashToCleanState(message?: string): Promise<boolean>
将所有更改（包括未跟踪文件）stash 到干净状态。

```typescript
export const stashToCleanState = async (message?: string): Promise<boolean>
```

**重要：** 先暂存未跟踪文件再 stash，防止数据丢失。

### preserveGitStateForIssue(): Promise<PreservedGitState | null>
为问题报告保存 Git 状态。

```typescript
export async function preserveGitStateForIssue(): Promise<PreservedGitState | null>
```

**包含：**
- 与远程分支的 merge-base SHA
- 从 merge-base 到当前状态的 patch
- 未跟踪文件及其内容
- format-patch 输出
- HEAD SHA 和分支名

**大小限制：**
- 单文件最大 500MB
- 总大小最大 5GB
- 最多 20000 个文件

### normalizeGitRemoteUrl(url: string): string | null
标准化 Git 远程 URL。

```typescript
export function normalizeGitRemoteUrl(url: string): string | null
```

**转换格式：**
- `git@github.com:owner/repo.git` -> `github.com/owner/repo`
- `https://github.com/owner/repo.git` -> `github.com/owner/repo`
- 统一为小写

### getRepoRemoteHash(): Promise<string | null>
获取仓库远程 URL 的 SHA256 哈希（前 16 字符）。

```typescript
export async function getRepoRemoteHash(): Promise<string | null>
```

**用途：**
- 相同的 SSH/HTTPS 克隆得到相同哈希
- 日志中不暴露实际仓库名

## 缓存函数

```typescript
gitExe(): string                    // 获取 git 可执行文件路径
getIsGit(): Promise<boolean>       // 是否在 Git 仓库中
getHead(): Promise<string>          // 获取当前 HEAD
getBranch(): Promise<string>        // 获取当前分支
getDefaultBranch(): Promise<string> // 获取默认分支
getRemoteUrl(): Promise<string | null>  // 获取远程 URL
getIsHeadOnRemote(): Promise<boolean>   // HEAD 是否在远程
hasUnpushedCommits(): Promise<boolean>  // 是否有未推送 commit
getIsClean(options?): Promise<boolean>  // 工作区是否干净
getChangedFiles(): Promise<string[]>     // 获取已更改文件
```

## 安全检查

### isCurrentDirectoryBareGitRepo()
检查当前目录是否看起来像裸露的 Git 仓库。

```typescript
export function isCurrentDirectoryBareGitRepo(): boolean
```

**安全目的：**
检测可能的恶意仓库攻击（攻击者创建 HEAD、objects/、refs/ 诱导执行 hooks）。

**检查：**
1. `.git/HEAD` 是否为有效文件
2. cwd 中是否有裸露仓库指标（HEAD、objects/、refs/）

## 诊断日志

关键操作都有诊断日志：
- `find_git_root_started` / `find_git_root_completed`
- `is_git_check_started` / `is_git_check_completed`

包含耗时和 stat 调用次数。
