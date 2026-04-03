# messages.ts - 消息处理系统

## 功能概述

`messages.ts` 是 Claude Code 中最核心的消息处理模块，负责：
- 创建各种类型的消息（assistant、user、system、progress 等）
- 处理消息内容和附件
- 管理 API 请求/响应
- 处理错误消息和拒绝消息

## 消息类型

### 核心类型导入
```typescript
import type {
  AssistantMessage,
  AttachmentMessage,
  Message,
  SystemMessage,
  UserMessage,
  // ... 更多
} from '../types/message.js'
```

## 常量

### 合成消息标记
```typescript
export const SYNTHETIC_MODEL = '<synthetic>'

export const SYNTHETIC_MESSAGES = new Set([
  INTERRUPT_MESSAGE,
  INTERRUPT_MESSAGE_FOR_TOOL_USE,
  CANCEL_MESSAGE,
  REJECT_MESSAGE,
  NO_RESPONSE_REQUESTED,
])
```

### 拒绝消息
```typescript
export const INTERRUPT_MESSAGE = '[Request interrupted by user]'
export const CANCEL_MESSAGE = "The user doesn't want to take this action right now..."
export const REJECT_MESSAGE = "The user doesn't want to proceed with this tool use..."
export const NO_RESPONSE_REQUESTED = 'No response requested.'
```

### 拒绝工作指南
```typescript
export const DENIAL_WORKAROUND_GUIDANCE = `IMPORTANT: You *may* attempt to accomplish this action using other tools...`
```

## 核心函数

### isSyntheticMessage(message: Message)
检查消息是否为合成消息。

```typescript
export function isSyntheticMessage(message: Message): boolean
```

### getLastAssistantMessage(messages: Message[])
获取最后一条 assistant 消息。

```typescript
export function getLastAssistantMessage(messages: Message[]): AssistantMessage | undefined
```

使用 `findLast` 从末尾开始查找，性能更好。

### hasToolCallsInLastAssistantTurn(messages: Message[])
检查最后一条 assistant 消息是否有工具调用。

```typescript
export function hasToolCallsInLastAssistantTurn(messages: Message[]): boolean
```

### isClassifierDenial(content: string)
检查工具结果消息是否为分类器拒绝。

```typescript
export function isClassifierDenial(content: string): boolean
```

### buildYoloRejectionMessage(reason: string)
为 YOLO 模式分类器拒绝构建消息。

```typescript
export function buildYoloRejectionMessage(reason: string): string
```

### buildClassifierUnavailableMessage(toolName: string, classifierModel: string)
构建分类器暂时不可用时的消息。

```typescript
export function buildClassifierUnavailableMessage(
  toolName: string,
  classifierModel: string,
): string
```

### withMemoryCorrectionHint(message: string)
为拒绝/取消消息添加记忆纠正提示。

```typescript
export function withMemoryCorrectionHint(message: string): string
```

**条件：**
- 自动记忆已启用
- GrowthBook flag `tengu_amber_prism` 为 true

### deriveShortMessageId(uuid: string)
从 UUID 派生短稳定的短消息 ID。

```typescript
export function deriveShortMessageId(uuid: string): string
```

**用途：**
- 工具引用中注入 `[id:...]` 标签
- 10 位十六进制转换为 6 位 base36

## 消息创建

### baseCreateAssistantMessage()
创建基础 assistant 消息。

```typescript
function baseCreateAssistantMessage({
  content,
  isApiErrorMessage = false,
  apiError,
  error,
  errorDetails,
  isVirtual,
  usage,
}: {
  content: BetaContentBlock[]
  isApiErrorMessage?: boolean
  apiError?: AssistantMessage['apiError']
  error?: SDKAssistantMessageError
  errorDetails?: string
  isVirtual?: true
  usage?: Usage
}): AssistantMessage
```

## 拒绝消息工厂函数

```typescript
export function AUTO_REJECT_MESSAGE(toolName: string): string
export function DONT_ASK_REJECT_MESSAGE(toolName: string): string
```

## 消息相关工具

**导入自其他模块：**
- `attachments.ts` - 附件处理
- `api.ts` - API 边界规范化
- `format.ts` - 格式化数字和 token
- `imageValidation.ts` - 图片验证
