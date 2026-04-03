# services/toolUseSummary - 工具使用摘要

## 功能

toolUseSummary 记录和汇总工具使用情况，用于分析和调试。

## 文件列表

| 文件 | 功能 |
|------|------|
| `toolUseSummaryGenerator.ts` | 摘要生成器 |

## 记录内容

```typescript
interface ToolUseSummary {
  toolName: string
  callCount: number
  totalDuration: number
  successRate: number
  averageInputTokens: number
  averageOutputTokens: number
  errors: ToolError[]
}
```

## 用途

- 使用统计
- 性能分析
- 异常检测
- 成本估算
