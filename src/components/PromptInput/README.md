# PromptInput/

## 功能
提示词输入框组件套件，是 Claude Code 的核心输入组件，处理用户的所有文本输入。

## 组件列表

- `PromptInput.tsx` - 核心输入框（355KB，最大组件）
- `PromptInputFooter.tsx` - 输入框页脚
- `PromptInputFooterLeftSide.tsx` - 页脚左侧
- `PromptInputFooterSuggestions.tsx` - 建议列表
- `PromptInputHelpMenu.tsx` - 帮助菜单
- `PromptInputModeIndicator.tsx` - 模式指示器
- `PromptInputQueuedCommands.tsx` - 队列命令
- `PromptInputStashNotice.tsx` - 暂存通知
- `HistorySearchInput.tsx` - 历史搜索输入
- `Notifications.tsx` - 通知组件
- `ShimmeredInput.tsx` - 闪烁输入效果
- `VoiceIndicator.tsx` - 语音指示器
- `SandboxPromptFooterHint.tsx` - Sandbox 提示
- `IssueFlagBanner.tsx` - 问题标记横幅

### Hooks 和工具
- `useSwarmBanner.ts` - Swarm 横幅 Hook
- `useShowFastIconHint.ts` - 快速图标提示 Hook
- `useMaybeTruncateInput.ts` - 输入截断 Hook
- `usePromptInputPlaceholder.ts` - 占位符 Hook
- `inputModes.ts` - 输入模式定义
- `inputPaste.ts` - 粘贴处理
- `utils.ts` - 工具函数

## 重要组件

### PromptInput
应用中最复杂的组件（355KB），负责：
- 用户文本输入
- 命令解析
- 自动补全
- 快捷键处理
- 多行输入
- 粘贴处理
- 模式切换（正常/特殊模式）

### PromptInputFooter
输入框下方的辅助区域：
- 模型选择器
- 快捷操作按钮
- 状态指示器

### PromptInputFooterSuggestions
根据上下文显示的建议：
- 基于历史的建议
- 工具建议
- 上下文相关建议
