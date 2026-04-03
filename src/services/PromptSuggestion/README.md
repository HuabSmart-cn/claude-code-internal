# services/PromptSuggestion - 提示建议

## 功能

PromptSuggestion 服务为用户推荐可能的输入提示，加快交互速度。

## 文件列表

| 文件 | 功能 | 大小 |
|------|------|------|
| `promptSuggestion.ts` | 建议生成 | 17KB |
| `speculation.ts` | 推测补全 | 30KB |

## 建议类型

### 1. 上下文相关建议
基于当前文件和项目状态推荐命令。

### 2. 历史建议
根据用户历史输入模式推荐。

### 3. 意图推测
`speculation.ts` 尝试预测用户意图并主动提供选项。

## 推测机制

```typescript
// speculation.ts
interface Speculation {
  intent: 'edit' | 'search' | 'execute' | 'explain'
  confidence: number           // 0-1
  suggestedPrompt: string
  reasoning: string
}
```

## 使用场景

- IDE 中输入时实时补全
- 命令行开头自动建议
- 对话中断后恢复建议
