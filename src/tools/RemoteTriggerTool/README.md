# RemoteTriggerTool

## 功能

管理远程触发器（Remote Agent Triggers）。

## 核心文件

- `RemoteTriggerTool.ts` - 主工具实现
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface RemoteTriggerInput {
  action: 'list' | 'get' | 'create' | 'update' | 'run'
  trigger_id?: string       // 触发器 ID
  body?: Record<string, unknown>  // 创建/更新时的 body
}
```

## 操作

- **list** - 列出所有触发器
- **get** - 获取触发器详情
- **create** - 创建新触发器
- **update** - 更新触发器
- **run** - 手动运行触发器

## 对应命令/用途

RemoteTriggerTool 用于远程触发 agent 任务。

**条件**：仅在 `AGENT_TRIGGERS_REMOTE` 功能开启时可用。
