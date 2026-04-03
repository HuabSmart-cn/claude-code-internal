# services/AgentSummary - Agent 摘要

## 功能

AgentSummary 提供当前 Agent 状态的结构化摘要。

## 文件列表

| 文件 | 功能 |
|------|------|
| `agentSummary.ts` | 摘要生成 |

## 摘要内容

```typescript
interface AgentSummary {
  agentId: string
  status: 'idle' | 'thinking' | 'executing' | 'waiting'
  currentTask?: Task
  recentActions: Action[]
  contextTokens: number
  availableTools: string[]
}
```

## 用途

- 调试和问题排查
- 状态可视化
- 会话恢复
