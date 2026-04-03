# messages/

## 功能
消息渲染目录，负责将 Claude Code 与用户的对话内容渲染成 UI。这是应用的核心 UI 层，包括：

- 用户消息（文本、图片、命令等）
- 助手消息（文本、思考过程、工具调用）
- 工具结果消息（成功、错误、拒绝、取消）
- 系统消息（API 错误、限流、关闭等）
- 附件渲染

## 组件列表

### 用户消息
- `UserTextMessage.tsx` - 用户文本消息
- `UserPlanMessage.tsx` - 用户计划消息
- `UserPromptMessage.tsx` - 用户提示消息
- `UserCommandMessage.tsx` - 用户命令消息
- `UserBashInputMessage.tsx` - Bash 输入消息
- `UserBashOutputMessage.tsx` - Bash 输出消息
- `UserChannelMessage.tsx` - 频道消息
- `UserImageMessage.tsx` - 图片消息
- `UserLocalCommandOutputMessage.tsx` - 本地命令输出
- `UserMemoryInputMessage.tsx` - 记忆输入消息
- `UserResourceUpdateMessage.tsx` - 资源更新消息
- `UserAgentNotificationMessage.tsx` - Agent 通知消息
- `UserTeammateMessage.tsx` - 队友消息

### 助手消息
- `AssistantTextMessage.tsx` - 助手文本消息
- `AssistantThinkingMessage.tsx` - 思考过程消息
- `AssistantRedactedThinkingMessage.tsx` - 已编辑的思考消息
- `AssistantToolUseMessage.tsx` - 工具调用消息
- `HighlightedThinkingText.tsx` - 高亮思考文本

### 工具结果消息 (UserToolResultMessage/)
- `UserToolResultMessage.tsx` - 工具结果消息容器
- `UserToolSuccessMessage.tsx` - 工具成功消息
- `UserToolErrorMessage.tsx` - 工具错误消息
- `UserToolRejectMessage.tsx` - 工具拒绝消息
- `UserToolCanceledMessage.tsx` - 工具取消消息
- `RejectedToolUseMessage.tsx` - 拒绝的工具使用
- `RejectedPlanMessage.tsx` - 拒绝的计划
- `utils.tsx` - 工具结果消息工具函数

### 系统消息
- `SystemTextMessage.tsx` - 系统文本消息
- `SystemAPIErrorMessage.tsx` - API 错误消息
- `RateLimitMessage.tsx` - 限流消息
- `ShutdownMessage.tsx` - 关闭消息
- `PlanApprovalMessage.tsx` - 计划审批消息
- `TaskAssignmentMessage.tsx` - 任务分配消息
- `AdvisorMessage.tsx` - 顾问/建议消息
- `HookProgressMessage.tsx` - Hook 进度消息

### 其他消息组件
- `AttachmentMessage.tsx` - 附件消息
- `CollapsedReadSearchContent.tsx` - 折叠的读写搜索内容
- `CompactBoundaryMessage.tsx` - 紧凑边界消息
- `GroupedToolUseContent.tsx` - 分组工具使用内容
- `ShutdownMessage.tsx` - 关闭消息

### 工具和状态
- `nullRenderingAttachments.ts` - 空附件渲染
- `teamMemCollapsed.tsx` - 团队记忆折叠
- `teamMemSaved.ts` - 团队记忆保存

## 重要组件

### AssistantToolUseMessage
核心组件，渲染助手发起的工具调用，包括：
- 工具名称和参数展示
- 工具执行状态（进行中、完成）
- 工具结果的展示区域

### SystemTextMessage
系统消息渲染，处理应用级别的通知和错误信息。

### UserToolResultMessage 子系统
完整的工具执行结果渲染系统，支持：
- 成功/错误/拒绝/取消四种状态
- Bash、Edit、Read 等不同工具的专用展示
- 差异对比（对于编辑操作）
