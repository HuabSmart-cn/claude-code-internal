# permissions/ - 权限管理系统

## 功能概述

`permissions/` 目录包含完整的权限管理系统，负责：
- 工具使用的权限检查
- 权限规则解析和匹配
- 权限决策（允许、拒绝、询问）
- 权限提示和解释

## 文件结构

```
permissions/
├── permissions.ts           # 核心权限检查逻辑
├── permissionSetup.ts       # 权限设置流程
├── permissionsLoader.ts     # 权限规则加载
├── permissionRuleParser.ts  # 规则解析
├── PermissionMode.ts        # 权限模式定义
├── PermissionResult.ts      # 权限结果类型
├── PermissionRule.ts        # 规则类型定义
├── PermissionUpdate.ts      # 权限更新
├── classifierDecision.ts   # 分类器决策
├── yoloClassifier.ts        # YOLO 模式分类器
├── autoModeState.ts         # 自动模式状态
├── bypassPermissionsKillswitch.ts  # 绕过权限开关
├── dangerousPatterns.ts     # 危险模式检测
├── denialTracking.ts       # 拒绝跟踪
├── filesystem.ts           # 文件系统权限
├── pathValidation.ts       # 路径验证
├── permissionExplainer.ts  # 权限解释
├── shellRuleMatching.ts    # Shell 规则匹配
├── shadowedRuleDetection.ts # 阴影规则检测
└── systemInit.ts           # 系统初始化
```

## 核心类型

### PermissionResult
```typescript
type PermissionResult =
  | { allowed: true }
  | { allowed: false; reason: string }
  | { ask: true; reason?: string }
```

### PermissionDecision
```typescript
type PermissionDecision =
  | { permitted: true }
  | PermissionDenyDecision
  | PermissionAskDecision
```

### PermissionRule
```typescript
type PermissionRule = {
  source: PermissionRuleSource
  ruleBehavior: 'allow' | 'deny' | 'ask'
  ruleValue: PermissionRuleValue
}
```

## 权限模式 (PermissionMode)

```typescript
enum PermissionMode {
  BUROCRATIC = 'bureaucratic'  // 需要明确批准
  BYPASS_PERMISSIONS = 'bypass' // 绕过权限（谨慎使用）
  YOLO = 'yolo'                 // 默认允许，分类器判断
}
```

## 权限规则来源

```typescript
const PERMISSION_RULE_SOURCES = [
  'cliArg',       // 命令行参数
  'command',      // 命令
  'session',      // 会话
  'settings',     // 设置文件
  'project',      // 项目设置
  'managed',      // 托管设置
] as const
```

## 核心函数

### getAllowRules(context: ToolPermissionContext)
获取所有允许规则。

```typescript
export function getAllowRules(context: ToolPermissionContext): PermissionRule[]
```

### getDenyRules(context: ToolPermissionContext)
获取所有拒绝规则。

```typescript
export function getDenyRules(context: ToolPermissionContext): PermissionRule[]
```

### getAskRules(context: ToolPermissionContext)
获取所有询问规则。

```typescript
export function getAskRules(context: ToolPermissionContext): PermissionRule[]
```

### toolAlwaysAllowedRule(context, tool)
检查工具是否在允许规则中。

```typescript
export function toolAlwaysAllowedRule(
  context: ToolPermissionContext,
  tool: Pick<Tool, 'name' | 'mcpInfo'>,
): PermissionRule | null
```

### getDenyRuleForTool(context, tool)
检查工具是否在拒绝规则中。

```typescript
export function getDenyRuleForTool(
  context: ToolPermissionContext,
  tool: Pick<Tool, 'name' | 'mcpInfo'>,
): PermissionRule | null
```

### toolMatchesRule(tool, rule)
检查工具是否匹配规则。

```typescript
function toolMatchesRule(
  tool: Pick<Tool, 'name' | 'mcpInfo'>,
  rule: PermissionRule,
): boolean
```

**匹配逻辑：**
- 直接工具名匹配
- MCP 服务器级权限：`mcp__server1` 匹配 `mcp__server1__tool1`
- 支持通配符：`mcp__server1__*`

### createPermissionRequestMessage(toolName, decisionReason?)
创建权限请求消息。

```typescript
export function createPermissionRequestMessage(
  toolName: string,
  decisionReason?: PermissionDecisionReason,
): string
```

**决策原因类型：**
- `classifier` - 分类器判断
- `hook` - Hook 阻塞
- `rule` - 规则要求
- `subcommandResults` - 子命令结果
- `permissionPromptTool` - 权限提示工具
- `sandboxOverride` - 沙箱覆盖
- `workingDir` - 工作目录
- `safetyCheck` - 安全检查
- `mode` - 权限模式

## 分类器

### YOLO 模式分类器
```typescript
export function classifyYoloAction(
  toolName: string,
  command: string,
): Promise<{ allowed: boolean; reason: string }>
```

### 分类器决策
```typescript
export async function classifyWithClassifier(
  toolName: string,
  command: string,
): Promise<PermissionDecision>
```

## 权限更新

### applyPermissionUpdate(rule: PermissionUpdate)
应用单个权限更新。

```typescript
export function applyPermissionUpdate(rule: PermissionUpdate): void
```

### persistPermissionUpdates(updates: PermissionUpdate[])
持久化权限更新到设置。

```typescript
export function persistPermissionUpdates(updates: PermissionUpdate[]): Promise<void>
```

## 危险模式检测

```typescript
export const DANGEROUS_PATTERNS = [
  // 文件操作
  /rm\s+(-rf\s+)?\//,                    // rm -rf /
  /dd\s+.*of=.*\//,                      // dd 写到根目录

  // 网络
  /curl.*\|.*sh/,                        // pipe curl to shell
  /wget.*\|.*sh/,                        // pipe wget to shell

  // 持久化
  /crontab.*-/                           // 覆盖 crontab
]
```

## 拒绝跟踪

跟踪拒绝次数，用于分类器回退。

```typescript
const DENIAL_LIMITS = {
  maxDenialsBeforeFallback: 3,           // 回退前最大拒绝次数
  denialWindowMs: 5 * 60 * 1000,        // 5 分钟窗口
}
```

## Shell 命令匹配

### extractOutputRedirections(cmd)
从命令中提取输出重定向。

```typescript
export function extractOutputRedirections(
  cmd: string,
): { commandWithoutRedirections: string; redirections: Redirection[] }
```

## 路径验证

### validatePath(path, context)
验证路径访问权限。

```typescript
export function validatePath(
  path: string,
  context: ToolPermissionContext,
): { valid: boolean; reason?: string }
```

## MCP 权限

MCP 工具使用 `mcp__server__tool` 命名格式。

```typescript
// MCP 服务器级权限
rule "mcp__server1" matches tool "mcp__server1__tool1"

// 通配符匹配
rule "mcp__server1__*" matches all tools from server1
```
