# query.ts

## 文件概述
**路径**: `src/query.ts`
**功能**: 核心查询循环，处理 AI 模型的流式响应、工具调用和上下文管理
**重要程度**: ★★★★★

---

## 核心概念
### 查询循环 (Query Loop)
Claude Code 的核心循环，处理：
1. 发送消息到 AI 模型
2. 接收流式响应
3. 执行工具调用
4. 处理压缩/上下文管理
5. 循环直到完成或达到终止条件

### 自动压缩 (Auto-compact)
当上下文接近 token 限制时，自动压缩历史消息。

### 流式工具执行 (Streaming Tool Execution)
允许在模型生成时并行执行工具调用。

### 查询参数 (QueryParams)
```typescript
type QueryParams = {
  messages: Message[]
  systemPrompt: SystemPrompt
  userContext: { [k: string]: string }
  systemContext: { [k: string]: string }
  canUseTool: CanUseToolFn
  toolUseContext: ToolUseContext
  fallbackModel?: string
  querySource: QuerySource
  maxOutputTokensOverride?: number
  maxTurns?: number
  skipCacheWrite?: boolean
  taskBudget?: { total: number }
}
```

---

## 主要类型/接口
```typescript
// 查询循环状态
type State = {
  messages: Message[]
  toolUseContext: ToolUseContext
  autoCompactTracking: AutoCompactTrackingState | undefined
  maxOutputTokensRecoveryCount: number
  hasAttemptedReactiveCompact: boolean
  maxOutputTokensOverride: number | undefined
  pendingToolUseSummary: Promise<ToolUseSummaryMessage | null> | undefined
  stopHookActive: boolean | undefined
  turnCount: number
  transition: Continue | undefined
}
```

---

## 关键函数
```typescript
/**
 * 主查询生成器
 * 产出类型：StreamEvent | RequestStartEvent | Message | TombstoneMessage | ToolUseSummaryMessage
 */
async function* query(params: QueryParams): AsyncGenerator<...>

/**
 * 查询循环内部实现
 */
async function* queryLoop(params: QueryParams, consumedCommandUuids: string[]): AsyncGenerator<...>
```

---

## 重要特性

### 思考块规则 (Thinking Block Rules)
1. 包含 thinking 或 redacted_thinking 的消息必须在 `max_thinking_length > 0` 的查询中
2. thinking 块不能是消息块的最后一个
3. thinking 块必须在整个 assistant 轨迹中保留

### 错误恢复机制
- `max_output_tokens` 错误恢复
- 模型降级（高负载时切换到备用模型）
- 上下文压缩恢复

---

## 与其他模块的关系
- 调用：
  - `query/tokenBudget.ts` - token 预算检查
  - `query/stopHooks.ts` - 停止钩子
  - `services/tools/toolOrchestration.js` - 工具编排
  - `services/compact/autoCompact.js` - 自动压缩
- 被调用：
  - `QueryEngine.ts` - SDK 查询
  - `REPL.tsx` - 交互式查询

---

## 英文对照词汇表
| English | 中文 |
|---------|------|
| Query | 查询 |
| Query loop | 查询循环 |
| Streaming | 流式 |
| Tool execution | 工具执行 |
| Auto-compact | 自动压缩 |
| Context collapse | 上下文折叠 |
| Thinking block | 思考块 |
| Recovery | 恢复 |
| Budget | 预算 |
| Turn | 轮次 |
