# tools/utils.ts - 工具消息处理辅助函数

## 功能

提供工具调用时消息标记和提取的辅助函数，用于处理消息的 transient 状态。

## 核心函数

### `tagMessagesWithToolUseID()`

```typescript
export function tagMessagesWithToolUseID(
  messages: (UserMessage | AttachmentMessage | SystemMessage)[],
  toolUseID: string | undefined,
): (UserMessage | AttachmentMessage | SystemMessage)[]
```

**功能**：为用户消息添加 `sourceToolUseID` 标记，使其在工具解析完成前保持 transient 状态。这可以防止 UI 中"is running"消息重复显示。

**参数**：
- `messages`: 要处理的消息数组
- `toolUseID`: 工具调用的 ID

**返回值**：添加了 sourceToolUseID 标记的消息数组

### `getToolUseIDFromParentMessage()`

```typescript
export function getToolUseIDFromParentMessage(
  parentMessage: AssistantMessage,
  toolName: string,
): string | undefined
```

**功能**：从父消息中提取指定工具的 tool use ID。

**参数**：
- `parentMessage`: Assistant 消息
- `toolName`: 工具名称

**返回值**：工具调用的 ID，如果未找到则返回 undefined
