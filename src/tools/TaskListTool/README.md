# TaskListTool

## 功能

列出所有任务（TodoV2 模式）。

## 核心文件

- `TaskListTool.ts` - 主工具实现
- `constants.ts` - 常量定义
- `prompt.ts` - 提示词

## 关键类型/函数

```typescript
interface TaskListOutput {
  tasks: Array<{
    id: string
    subject: string
    status: TaskStatus
    owner?: string
    blockedBy: string[]
  }>
}
```

## 对应命令/用途

TaskList 用于查看当前所有任务的状态。

**条件**：仅在 `isTodoV2Enabled()` 时可用。
