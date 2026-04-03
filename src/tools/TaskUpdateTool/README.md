# TaskUpdateTool

## 功能

更新任务状态和属性（TodoV2 模式）。

## 核心文件

- `TaskUpdateTool.ts` - 主工具实现
- `constants.ts` - 常量定义
- `prompt.ts` - 提示词

## 关键类型/函数

```typescript
interface TaskUpdateInput {
  taskId: string
  subject?: string
  description?: string
  activeForm?: string
  status?: TaskStatus | 'deleted'
  addBlocks?: string[]       // 此任务阻塞的任务
  addBlockedBy?: string[]    // 阻塞此任务的任务
  owner?: string
  metadata?: Record<string, unknown>
}
```

## 对应命令/用途

TaskUpdate 用于修改任务状态、设置依赖关系。

**条件**：仅在 `isTodoV2Enabled()` 时可用。
