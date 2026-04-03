# Tool.ts

## 文件概述
**路径**: `src/Tool.ts`
**功能**: 定义工具(Tool)的类型系统、接口和构建器
**重要程度**: ★★★★★

---

## 核心概念
### Tool (工具)
Claude Code 的核心抽象，表示可以被 AI 模型调用的工具。每个工具包含：
- 输入/输出模式 (Zod schema)
- 权限检查
- 渲染逻辑
- 进度显示

### ToolUseContext (工具使用上下文)
贯穿整个查询生命周期的大型上下文对象，包含：
- AppState 访问
- AbortController
- MCP 客户端
- 权限上下文
- 消息历史
- 各种回调函数

### ToolPermissionContext (工具权限上下文)
```typescript
type ToolPermissionContext = DeepImmutable<{
  mode: PermissionMode
  additionalWorkingDirectories: Map<string, AdditionalWorkingDirectory>
  alwaysAllowRules: ToolPermissionRulesBySource
  alwaysDenyRules: ToolPermissionRulesBySource
  alwaysAskRules: ToolPermissionRulesBySource
  isBypassPermissionsModeAvailable: boolean
  isAutoModeAvailable?: boolean
  // ...
}>
```

---

## 主要类型/接口
```typescript
// 工具定义
type Tool<
  Input extends AnyObject = AnyObject,
  Output = unknown,
  P extends ToolProgressData = ToolProgressData,
> = {
  name: string
  inputSchema: Input
  aliases?: string[]                    // 向后兼容别名
  searchHint?: string                   // ToolSearch 关键词匹配
  call(
    args: z.infer<Input>,
    context: ToolUseContext,
    canUseTool: CanUseToolFn,
    parentMessage: AssistantMessage,
    onProgress?: ToolCallProgress<P>
  ): Promise<ToolResult<Output>>
  description(): Promise<string>
  isConcurrencySafe(): boolean
  isEnabled(): boolean
  isReadOnly(): boolean
  isDestructive?(): boolean
  interruptBehavior?(): 'cancel' | 'block'
  validateInput?(): Promise<ValidationResult>
  checkPermissions(): Promise<PermissionResult>
  renderToolResultMessage?(): React.ReactNode
  renderToolUseMessage(): React.ReactNode
  // ... 更多可选方法
}

// 工具集合类型
type Tools = readonly Tool[]

// 工具结果
type ToolResult<T> = {
  data: T
  newMessages?: Array<UserMessage | AssistantMessage | AttachmentMessage | SystemMessage>
  contextModifier?: (context: ToolUseContext) => ToolUseContext
  mcpMeta?: { _meta?: Record<string, unknown>; structuredContent?: Record<string, unknown> }
}
```

---

## 关键函数
```typescript
/**
 * 构建完整工具，填充默认值
 * 默认值：
 * - isEnabled: true
 * - isConcurrencySafe: false
 * - isReadOnly: false
 * - isDestructive: false
 * - checkPermissions: allow
 * - toAutoClassifierInput: ''
 * - userFacingName: name
 */
function buildTool<D extends AnyToolDef>(def: D): BuiltTool<D>

/**
 * 查找工具（按名称或别名）
 */
function findToolByName(tools: Tools, name: string): Tool | undefined

/**
 * 检查工具是否匹配名称
 */
function toolMatchesName(tool: { name: string; aliases?: string[] }, name: string): boolean
```

---

## 与其他模块的关系
- 被调用：
  - `tools.ts` - 获取所有工具
  - `query.ts` - 工具执行
  - `QueryEngine.ts` - SDK 工具调用
  - `ToolUseContext` 贯穿整个查询系统

---

## 英文对照词汇表
| English | 中文 |
|---------|------|
| Tool | 工具 |
| ToolUseContext | 工具使用上下文 |
| ToolPermissionContext | 工具权限上下文 |
| ToolResult | 工具结果 |
| InputSchema | 输入模式 |
| OutputSchema | 输出模式 |
| Validation | 验证 |
| Permission | 权限 |
| Concurrency | 并发性 |
| buildTool | 构建工具 |
| alias | 别名 |
