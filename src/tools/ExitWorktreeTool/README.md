# ExitWorktreeTool

## 功能

退出 git worktree，返回原目录。

## 核心文件

- `ExitWorktreeTool.ts` - 主工具实现
- `constants.ts` - 常量定义
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface ExitWorktreeInput {
  action: 'keep' | 'remove'  // 保留或删除 worktree
  discard_changes?: boolean   // 是否放弃未提交更改
}
```

## 特性

- **保留选项** - keep: 保留 worktree 和分支
- **删除选项** - remove: 删除 worktree 和分支
- **更改检查** - 删除时检查未提交更改

## 对应命令/用途

ExitWorktreeTool 用于完成 worktree 工作后清理。

**条件**：仅在 `isWorktreeModeEnabled()` 时可用。

**相关工具**：EnterWorktreeTool
