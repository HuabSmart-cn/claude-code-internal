# EnterWorktreeTool

## 功能

创建 git worktree 并切换到其中。

## 核心文件

- `EnterWorktreeTool.ts` - 主工具实现
- `constants.ts` - 常量定义
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface EnterWorktreeInput {
  name?: string              // worktree 名称（可选，自动生成）
}
```

## 特性

- **自动生成名称** - 未提供时随机生成
- **工作目录切换** - 自动切换到新 worktree
- **会话状态保存** - 保存 worktree 状态

## 对应命令/用途

EnterWorktreeTool 用于在隔离的 git worktree 中工作，避免干扰主分支。

**条件**：仅在 `isWorktreeModeEnabled()` 时可用。

**相关工具**：ExitWorktreeTool
