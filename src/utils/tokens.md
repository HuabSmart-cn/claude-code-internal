# tokens.ts - Token 计算与统计

## 功能概述

`tokens.ts` 负责计算和管理 Claude API 调用的 token 使用情况。这是 Claude Code 中 token 统计的核心模块。

## 核心函数

### getTokenUsage(message: Message)
从 assistant 消息中提取 API 使用数据。

```typescript
export function getTokenUsage(message: Message): Usage | undefined
```

**逻辑：**
- 检查消息是否为 assistant 类型
- 检查是否有 `usage` 字段
- 排除合成消息（SYNTHETIC_MESSAGES）
- 排除合成模型（SYNTHETIC_MODEL）

### getTokenCountFromUsage(usage: Usage)
计算上下文窗口的总 token 数。

```typescript
export function getTokenCountFromUsage(usage: Usage): number
```

**公式：**
```
input_tokens + cache_creation_input_tokens + cache_read_input_tokens + output_tokens
```

### tokenCountFromLastAPIResponse(messages: Message[])
从最后一条 API 响应获取上下文大小。

```typescript
export function tokenCountFromLastAPIResponse(messages: Message[]): number
```

### tokenCountWithEstimation(messages: readonly Message[])
**最重要的函数** - 获取当前上下文窗口大小。

这是用于检查阈值（自动压缩、会话内存初始化等）的标准函数。使用最后一个 API 响应的 token 数（input + output + cache）加上对后续消息的估算。

**关键特性：**
- 处理并行工具调用：当模型在一个响应中发出多个工具调用时，流式代码为每个内容块发出单独的 assistant 记录
- 通过 `message.id` 识别同一次 API 响应分割的记录
- 正确估算所有交错工具调用的 token

```typescript
export function tokenCountWithEstimation(messages: readonly Message[]): number
```

**算法：**
1. 从最后一条消息向前查找有 usage 的记录
2. 如果找到，检查是否有同 id 的早期记录（并行工具调用分割）
3. 如果有，向后走到第一条同 id 记录
4. 返回 usage token 数 + 后续消息的估算

### getAssistantMessageContentLength(message: AssistantMessage)
计算 assistant 消息的内容长度（字符数）。

```typescript
export function getAssistantMessageContentLength(message: AssistantMessage): number
```

**计数内容：**
- text（text_delta）
- thinking（thinking_delta）
- redacted_thinking data
- tool_use input（input_json_delta）
- 排除 signature_delta（不是模型输出）

### getCurrentUsage(messages: Message[])
获取当前使用统计。

```typescript
export function getCurrentUsage(messages: Message[]): {
  input_tokens: number
  output_tokens: number
  cache_creation_input_tokens: number
  cache_read_input_tokens: number
} | null
```

### messageTokenCountFromLastAPIResponse(messages: Message[])
仅获取最后响应的 output_tokens。

**警告：** 不要用于阈值比较，使用 `tokenCountWithEstimation()` 代替。

## 常量

```typescript
export const SYNTHETIC_MESSAGES = new Set([
  INTERRUPT_MESSAGE,
  INTERRUPT_MESSAGE_FOR_TOOL_USE,
  CANCEL_MESSAGE,
  REJECT_MESSAGE,
  NO_RESPONSE_REQUESTED,
])

export const SYNTHETIC_MODEL = '<synthetic>'
```

## 导入依赖

- `@anthropic-ai/sdk/resources/beta/messages/messages.mjs` - SDK 类型
- `../services/tokenEstimation.js` - 估算函数
- `../types/message.js` - 消息类型
- `./messages.js` - SYNTHETIC_MESSAGES, SYNTHETIC_MODEL
- `./slowOperations.js` - jsonStringify
