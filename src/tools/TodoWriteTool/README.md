# TodoWriteTool

## 功能

管理 session 的任务列表（待办事项）。

## 核心文件

- `TodoWriteTool.ts` - 主工具实现
- `constants.ts` - 常量定义
- `prompt.ts` - 提示词

## 关键类型/函数

```typescript
interface TodoWriteInput {
  todos: Array<{
    status: 'pending' | 'in_progress' | 'completed' | 'cancelled'
    activeForm?: string      // 进行中的描述
    content: string          // 任务内容
  }>
}
```

## 特性

- **状态跟踪** - pending、in_progress、completed、cancelled
- **验证催促** - 验证代理可能需要的提示
- **V2 切换** - V2 启用时禁用（使用 Task* 工具）

## 对应命令/用途

TodoWrite 用于 AI 内部跟踪任务进度，用户可以通过 UI 看到。

**注意**：V2 模式（isTodoV2Enabled）下使用 Task* 工具替代。
