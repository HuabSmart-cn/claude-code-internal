# TaskStopTool

## 功能

停止正在运行的后台任务。

## 核心文件

- `TaskStopTool.ts` - 主工具实现
- `constants.ts` - 常量定义
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface TaskStopInput {
  task_id?: string           // 要停止的任务 ID
  shell_id?: string          // 废弃：使用 task_id
}
```

## 特性

- **别名支持** - 支持旧名 KillShell（向后兼容）
- **延迟加载** - shouldDefer: true

## 对应命令/用途

TaskStop 用于停止不再需要的后台任务，释放资源。
