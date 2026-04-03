# ScheduleCronTool

## 功能

创建、删除和列出定时任务。

## 核心文件

- `CronCreateTool.ts` - 创建定时任务
- `CronDeleteTool.ts` - 删除定时任务
- `CronListTool.ts` - 列出定时任务
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## CronCreateTool

```typescript
interface CronCreateInput {
  cron: string               // 5 字段 cron 表达式
  prompt: string             // 触发时执行的提示
  recurring?: boolean        // 是否重复
  durable?: boolean         // 是否持久化
}
```

## CronDeleteTool

```typescript
interface CronDeleteInput {
  id: string                 // 要删除的任务 ID
}
```

## CronListTool

无输入参数，返回所有定时任务。

## 对应命令/用途

ScheduleCronTool 用于定时执行任务，如定期提醒、持续集成等。

**条件**：仅在 `AGENT_TRIGGERS` 功能开启时可用。
