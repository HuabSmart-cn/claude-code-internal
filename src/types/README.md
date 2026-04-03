# types

## 功能
类型定义目录，包含核心 TypeScript 类型定义文件以及由 Protocol Buffers 生成的类型。

## 文件列表 (根目录 - 7个文件)

- `command.ts` - 命令/技能类型定义
  - `LocalCommandResult` - 本地命令执行结果
  - `PromptCommand` - 提示类命令定义
  - `LocalCommand` / `LocalCommandModule` - 本地命令模块
  - `LocalJSXCommandCall` / `LocalJSXCommandModule` - JSX 命令类型
  - `CommandBase` - 命令基类，包含 availability、isEnabled、isHidden 等属性
  - `CommandAvailability` - 可用性要求 ('claude-ai' | 'console')

- `hooks.ts` - Hook 系统类型定义
  - `HookEvent` 相关类型和 `HOOK_EVENTS` 常量
  - `promptRequestSchema` / `PromptRequest` / `PromptResponse` - 提示请求协议
  - `syncHookResponseSchema` / `hookJSONOutputSchema` - Hook 响应模式
  - `HookCallback` / `HookCallbackMatcher` - Hook 回调类型
  - `HookResult` / `AggregatedHookResult` - Hook 执行结果
  - 类型守卫函数: `isSyncHookJSONOutput()` / `isAsyncHookJSONOutput()`

- `permissions.ts` - 权限类型定义
  - `EXTERNAL_PERMISSION_MODES` / `INTERNAL_PERMISSION_MODES` - 权限模式常量
  - `PermissionMode` / `InternalPermissionMode` - 权限模式类型
  - `PermissionBehavior` - 权限行为 ('allow' | 'deny' | 'ask')
  - `PermissionRule` - 权限规则类型

- `plugin.ts` - 插件系统类型定义
  - `PluginManifest` / `PluginAuthor` / `CommandMetadata` - 插件清单类型
  - `BuiltinPluginDefinition` - 内置插件定义
  - `PluginRepository` / `PluginConfig` - 插件仓库配置
  - `LoadedPlugin` - 已加载插件类型
  - `PluginError` - 插件错误类型（ discriminated union，28种错误类型）
  - `getPluginErrorMessage()` - 错误消息辅助函数

- `textInputTypes.ts` - 文本输入类型定义
  - `InlineGhostText` - 命令自动补全的幽灵文本
  - `BaseTextInputProps` / `VimTextInputProps` - 输入组件属性
  - `VimMode` - Vim 模式 ('INSERT' | 'NORMAL')
  - `TextInputState` / `VimInputState` - 输入状态类型
  - `QueuedCommand` - 队列命令类型
  - `QueuePriority` - 队列优先级 ('now' | 'next' | 'later')

- `logs.ts` - 日志类型定义

- `ids.ts` - ID 类型定义

## generated/ 子目录

由 Protocol Buffers 生成的类型文件，使用 `protoc-gen-ts_proto` 生成。

### generated/enums.ts
生成的枚举类型

### generated/index.ts
主生成类型入口文件

### generated/events_mono/
事件相关生成类型

- `events_mono/claude_code/v1/` - Claude Code 事件类型
- `events_mono/common/v1/` - 通用事件类型
- `events_mono/growthbook/v1/` - GrowthBook 分析事件类型

### generated/google/protobuf/
Google Protocol Buffers 标准类型

- `google/protobuf/timestamp.ts` - 时间戳类型
  - 由 `protoc-gen-ts_proto` 生成
  - 表示独立于时区和本地日历的时间点
  - 编码为自 UTC 1970-01-01 以来的秒数和纳秒分数

## 核心概念

### 命令类型系统
Claude Code 使用分层命令架构：
- `PromptCommand` - 需要模型推理的命令
- `LocalCommand` - 本地执行的命令
- `LocalJSXCommand` - React JSX 组件命令

### Hook 系统
支持同步和异步两种 Hook 响应类型，通过 `hookJSONOutputSchema` 进行 Zod 验证。

### 插件错误处理
使用 discriminated union 类型 `PluginError`，提供类型安全的错误处理，避免字符串匹配的错误方式。
