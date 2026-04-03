# TaskOutputTool

## 功能

获取后台任务的输出。

## 核心文件

- `TaskOutputTool.tsx` - 主工具实现（React 组件）
- `constants.ts` - 常量定义

## 关键类型/函数

```typescript
interface TaskOutputInput {
  task_id: string
  block?: boolean            // 是否等待完成
  timeout?: number           // 超时毫秒
}

interface TaskOutput {
  task_id: string
  task_type: TaskType
  status: string
  description: string
  output: string
  exitCode?: number
  error?: string
  prompt?: string
  result?: string
}
```

## 对应命令/用途

TaskOutput 用于获取正在运行或已完成任务的输出。
