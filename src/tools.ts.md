# tools.ts

## 文件概述
**路径**: `src/tools.ts`
**功能**: 工具注册、过滤和获取的入口点
**重要程度**: ★★★★★

---

## 核心概念
### 工具预设 (Tool Presets)
支持 `--tools` 参数的预定义工具集：
- `default`: 默认工具集

### 工具过滤
- 按权限规则过滤
- 按模式过滤（如 REPL 模式隐藏原始工具）
- 按功能标志过滤

### 工具池组装
组合内置工具和 MCP 工具，确保：
1. 正确去重
2. 排序稳定（用于 prompt 缓存）

---

## 主要工具列表
```typescript
const baseTools = [
  AgentTool,
  TaskOutputTool,
  BashTool,
  GlobTool,           // 无嵌入式搜索时
  GrepTool,          // 无嵌入式搜索时
  ExitPlanModeV2Tool,
  FileReadTool,
  FileEditTool,
  FileWriteTool,
  NotebookEditTool,
  WebFetchTool,
  TodoWriteTool,
  WebSearchTool,
  TaskStopTool,
  AskUserQuestionTool,
  SkillTool,
  EnterPlanModeTool,
  // 条件工具...
]
```

---

## 关键函数
```typescript
/**
 * 获取所有可能可用的工具（不考虑权限过滤）
 */
function getAllBaseTools(): Tools

/**
 * 根据权限上下文获取工具
 */
function getTools(permissionContext: ToolPermissionContext): Tools

/**
 * 组合内置工具和 MCP 工具
 */
function assembleToolPool(
  permissionContext: ToolPermissionContext,
  mcpTools: Tools
): Tools

/**
 * 获取合并后的完整工具列表
 */
function getMergedTools(
  permissionContext: ToolPermissionContext,
  mcpTools: Tools
): Tools

/**
 * 按拒绝规则过滤工具
 */
function filterToolsByDenyRules<T>(tools: readonly T[], permissionContext: ToolPermissionContext): T[]

/**
 * 解析工具预设
 */
function parseToolPreset(preset: string): ToolPreset | null
```

---

## 与其他模块的关系
- 调用：
  - `Tool.ts` - 工具类型定义
  - 各种工具实现
  - `utils/permissions/permissions.ts` - 权限过滤
- 被调用：
  - `main.tsx` - 初始化
  - `query.ts` - 获取工具列表
  - `QueryEngine.ts` - SDK 工具

---

## 英文对照词汇表
| English | 中文 |
|---------|------|
| Tools | 工具 |
| Tool preset | 工具预设 |
| Tool pool | 工具池 |
| Filter | 过滤 |
| Assemble | 组装 |
| MCP tools | MCP 工具 |
| Built-in tools | 内置工具 |
| Permission rules | 权限规则 |
