# context.ts

## 文件概述
**路径**: `src/context.ts`
**功能**: 提供系统上下文和用户上下文的获取与管理
**重要程度**: ★★★★☆

---

## 核心概念
### 系统上下文 (System Context)
在每次对话开头预置的信息，包括：
- Git 状态（分支、状态、最近提交）
- 系统提示注入（用于缓存破坏）

### 用户上下文 (User Context)
- CLAUDE.md 文件内容
- 当前日期

---

## 关键函数
```typescript
/**
 * 获取 Git 状态（带缓存）
 * 返回格式：
 * - 当前分支
 * - 主分支（用于 PR）
 * - Git 用户名
 * - 状态（截断到 2000 字符）
 * - 最近 5 条提交
 */
const getGitStatus = memoize(async (): Promise<string | null>)

/**
 * 获取系统上下文（带缓存）
 * 包含 gitStatus 和可能的 cacheBreaker
 */
const getSystemContext = memoize(async (): Promise<{ [k: string]: string }>)

/**
 * 获取用户上下文（带缓存）
 * 包含 claudeMd 和 currentDate
 */
const getUserContext = memoize(async (): Promise<{ [k: string]: string }>)

/**
 * 设置系统提示注入（用于缓存破坏，ant-only）
 */
function setSystemPromptInjection(value: string | null): void
```

---

## 重要常量
```typescript
const MAX_STATUS_CHARS = 2000  // Git 状态最大字符数
```

---

## 与其他模块的关系
- 调用：
  - `utils/git.js` - Git 操作
  - `utils/claudemd.js` - CLAUDE.md 读取
  - `bootstrap/state.js` - 状态管理
- 被调用：
  - `main.tsx` - 预取系统上下文
  - `query.ts` - 获取上下文
  - `QueryEngine.ts` - SDK 查询

---

## 英文对照词汇表
| English | 中文 |
|---------|------|
| System context | 系统上下文 |
| User context | 用户上下文 |
| Git status | Git 状态 |
| Git branch | Git 分支 |
| CLAUDE.md | 项目配置文件 |
| Cache breaker | 缓存破坏器 |
| memoize | 记忆化 |
