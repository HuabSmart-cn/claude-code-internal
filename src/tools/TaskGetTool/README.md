# TaskGetTool

## 功能

获取单个任务的详情（TodoV2 模式）。

## 核心文件

- `TaskGetTool.ts` - 主工具实现
- `constants.ts` - 常量定义
- `prompt.ts` - 提示词

## 关键类型/函数

```typescript
interface TaskGetInput {
  taskId: string
}

interface TaskGetOutput {
  task: {
    id: string
    subject: string
    description: string
    status: TaskStatus
    blocks: string[]
    blockedBy: string[]
  } | null
}
```

## 对应命令/用途

TaskGet 用于获取特定任务的详细信息。

**条件**：仅在 `isTodoV2Enabled()` 时可用。
