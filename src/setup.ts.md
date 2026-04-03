# setup.ts

## 文件概述
**路径**: `src/setup.ts`
**功能**: 应用启动时的初始化设置，包括工作区创建、权限配置、插件加载等
**重要程度**: ★★★★★

---

## 核心概念
### 工作区模式 (Worktree Mode)
Claude Code 支持在 git worktree 中运行，每个 worktree 有独立的目录和分支。

### 权限模式 (Permission Mode)
- `default`: 默认权限模式
- `bypassPermissions`: 绕过权限检查
- `plan`: 计划模式

### UDS 消息服务器
Unix Domain Socket 消息服务器，用于进程间通信。

---

## 关键函数
```typescript
/**
 * 主设置函数
 * 执行顺序：
 * 1. Node.js 版本检查
 * 2. 自定义会话 ID 设置
 * 3. UDS 消息服务器启动
 * 4. 终端备份恢复 (iTerm2/Terminal.app)
 * 5. 工作目录设置
 * 6. Hooks 配置快照
 * 7. 文件变更监视器初始化
 * 8. Worktree 创建（如果启用）
 * 9. 后台任务初始化
 * 10. 插件预加载
 * 11. API Key 预取
 * 12. 发布说明检查
 */
async function setup(
  cwd: string,
  permissionMode: PermissionMode,
  allowDangerouslySkipPermissions: boolean,
  worktreeEnabled: boolean,
  worktreeName: string | undefined,
  tmuxEnabled: boolean,
  customSessionId?: string | null,
  worktreePRNumber?: number,
  messagingSocketPath?: string,
): Promise<void>
```

---

## 重要检查项
- Node.js 版本 >= 18
- 非 root/sudo 用户（除非在沙箱中）
- Docker/沙箱环境检查

---

## 与其他模块的关系
- 调用：
  - `bootstrap/state.js` - 状态管理
  - `utils/worktree.ts` - worktree 创建
  - `utils/hooks/hooksConfigSnapshot.ts` - hooks 快照
  - `utils/plugins/loadPluginHooks.js` - 插件 hooks
- 被调用：`main.tsx` - 应用入口

---

## 英文对照词汇表
| English | 中文 |
|---------|------|
| Setup | 设置 |
| Permission mode | 权限模式 |
| Worktree | 工作树 |
| Tmux | Tmux 会话管理 |
| Messaging socket | 消息套接字 |
| Hooks snapshot | Hooks 快照 |
| Pre-fetch | 预取 |
| Sandbox | 沙箱 |
| Docker | Docker 容器 |
