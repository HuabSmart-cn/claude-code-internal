# tools.ts - 工具系统主入口

## 功能

Claude Code 的**工具注册中心**，负责：
1. 导入和注册所有内置工具
2. 根据功能开关（feature flags）条件性地包含/排除工具
3. 提供工具过滤（权限、REPL 模式等）
4. 组装完整的工具池（内置 + MCP 工具）

## 核心架构

### 工具接口（Tool Interface）

所有工具都实现 `Tool` 接口（定义在 `src/Tool.ts`），核心属性：

```typescript
interface Tool<Input, Output, P extends ToolProgressData> {
  name: string              // 工具唯一名称
  aliases?: string[]        // 向后兼容的别名
  inputSchema: Input        // Zod 输入模式
  outputSchema: Output      // Zod 输出模式
  searchHint?: string        // ToolSearch 关键字匹配提示

  // 核心方法
  call(args, context, canUseTool, parentMessage, onProgress?): Promise<ToolResult<Output>>
  description(input, options): Promise<string>
  prompt(options): Promise<string>

  // 状态方法
  isEnabled(): boolean
  isConcurrencySafe(input): boolean
  isReadOnly(input): boolean
  isDestructive?(input): boolean
  interruptBehavior?(): 'cancel' | 'block'
  shouldDefer?: boolean     // 是否延迟加载
  alwaysLoad?: boolean      // 始终加载（不被 ToolSearch 延迟）
}
```

### `buildTool` 工厂函数

使用 `buildTool()` 创建工具，自动填充默认值：

```typescript
const TOOL_DEFAULTS = {
  isEnabled: () => true,
  isConcurrencySafe: (_input) => false,
  isReadOnly: (_input) => false,
  isDestructive: (_input) => false,
  checkPermissions: (input) => ({ behavior: 'allow', updatedInput: input }),
  toAutoClassifierInput: () => '',
  userFacingName: () => name,
}
```

## 工具注册表

### 内置工具（无条件加载）

| 工具 | 文件 | 功能 |
|------|------|------|
| `AgentTool` | `AgentTool/AgentTool.tsx` | 启动子代理执行任务 |
| `BashTool` | `BashTool/BashTool.tsx` | 执行 shell 命令 |
| `FileReadTool` | `FileReadTool/FileReadTool.ts` | 读取文件内容 |
| `FileEditTool` | `FileEditTool/FileEditTool.ts` | 编辑文件（diff） |
| `FileWriteTool` | `FileWriteTool/FileWriteTool.ts` | 写入文件 |
| `GlobTool` | `GlobTool/GlobTool.ts` | 文件名模式匹配 |
| `GrepTool` | `GrepTool/GrepTool.ts` | 正则表达式搜索 |
| `WebSearchTool` | `WebSearchTool/WebSearchTool.ts` | 网络搜索 |
| `WebFetchTool` | `WebFetchTool/WebFetchTool.ts` | 获取网页内容 |
| `TodoWriteTool` | `TodoWriteTool/TodoWriteTool.ts` | 管理 todo 列表 |
| `TaskStopTool` | `TaskStopTool/TaskStopTool.ts` | 停止后台任务 |
| `BriefTool` | `BriefTool/BriefTool.ts` | 向用户发送消息 |
| `AskUserQuestionTool` | `AskUserQuestionTool/AskUserQuestionTool.tsx` | 向用户提问 |
| `SkillTool` | `SkillTool/SkillTool.ts` | 执行 skill 命令 |
| `EnterPlanModeTool` | `EnterPlanModeTool/EnterPlanModeTool.ts` | 进入计划模式 |
| `ExitPlanModeV2Tool` | `ExitPlanModeTool/ExitPlanModeV2Tool.ts` | 退出计划模式 |
| `ListMcpResourcesTool` | `ListMcpResourcesTool/ListMcpResourcesTool.ts` | 列出 MCP 资源 |
| `ReadMcpResourceTool` | `ReadMcpResourceTool/ReadMcpResourceTool.ts` | 读取 MCP 资源 |
| `ToolSearchTool` | `ToolSearchTool/ToolSearchTool.ts` | 搜索延迟加载的工具 |

### 条件性工具（根据 feature flags）

| 工具 | 条件 | 功能 |
|------|------|------|
| `ConfigTool` | `USER_TYPE === 'ant'` | 读取/写入配置 |
| `TungstenTool` | `USER_TYPE === 'ant'` | Ant 专用工具 |
| `REPLTool` | `USER_TYPE === 'ant'` | REPL 包装器 |
| `LSPTool` | `ENABLE_LSP_TOOL` | 语言服务器协议 |
| `EnterWorktreeTool` | `worktreeModeEnabled()` | 创建 git worktree |
| `ExitWorktreeTool` | `worktreeModeEnabled()` | 退出 git worktree |
| `TeamCreateTool` | `agentSwarmsEnabled()` | 创建 agent 团队 |
| `TeamDeleteTool` | `agentSwarmsEnabled()` | 删除 agent 团队 |
| `TaskCreateTool` | `isTodoV2Enabled()` | 创建任务 |
| `TaskGetTool` | `isTodoV2Enabled()` | 获取任务详情 |
| `TaskUpdateTool` | `isTodoV2Enabled()` | 更新任务 |
| `TaskListTool` | `isTodoV2Enabled()` | 列出所有任务 |
| `SleepTool` | `PROACTIVE` 或 `KAIROS` | 延迟执行 |
| `SendMessageTool` | 动态加载 | 团队成员间通信 |
| `PowerShellTool` | `isPowerShellToolEnabled()` | PowerShell 支持 |
| `MonitorTool` | `MONITOR_TOOL` | 监控工具 |
| `RemoteTriggerTool` | `AGENT_TRIGGERS_REMOTE` | 远程触发器 |
| `CronCreateTool` | `AGENT_TRIGGERS` | 创建定时任务 |
| `CronDeleteTool` | `AGENT_TRIGGERS` | 删除定时任务 |
| `CronListTool` | `AGENT_TRIGGERS` | 列出定时任务 |
| `WebBrowserTool` | `WEB_BROWSER_TOOL` | 网页浏览器 |
| `SnipTool` | `HISTORY_SNIP` | 历史截取 |
| `ListPeersTool` | `UDS_INBOX` | 列出对等节点 |
| `WorkflowTool` | `WORKFLOW_SCRIPTS` | 工作流脚本 |

## 核心 API

### `getAllBaseTools()`

返回所有可能可用的工具列表（考虑环境标志）。

```typescript
export function getAllBaseTools(): Tools
```

### `getTools(permissionContext)`

获取在给定权限上下文中的可用工具。

```typescript
export function getTools(permissionContext: ToolPermissionContext): Tools
```

### `filterToolsByDenyRules(tools, permissionContext)`

根据拒绝规则过滤工具。

### `assembleToolPool(permissionContext, mcpTools)`

组装完整的工具池（内置 + MCP）。

```typescript
export function assembleToolPool(
  permissionContext: ToolPermissionContext,
  mcpTools: Tools,
): Tools
```

### `getMergedTools(permissionContext, mcpTools)`

获取合并后的工具列表（含 MCP 工具）。

### Simple 模式

当 `CLAUDE_CODE_SIMPLE` 环境变量设置时，仅返回：
- `BashTool`
- `FileReadTool`
- `FileEditTool`

（协调器模式下额外包含 `AgentTool`, `TaskStopTool`, `SendMessageTool`）

## 延迟加载（Tool Deferral）

`shouldDefer: true` 的工具不会在首次提示中包含，需要通过 `ToolSearchTool` 搜索后才能调用。这用于减少初始上下文大小。

`alwaysLoad: true` 的工具始终加载，不受 ToolSearch 影响。

## REPL 模式

当 REPL 模式启用时，某些原始工具被隐藏在 REPL 包装器内部，但通过 VM 上下文仍然可访问。
