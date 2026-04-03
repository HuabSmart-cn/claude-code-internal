# MCPTool

## 功能

执行 Model Context Protocol (MCP) 服务器提供的工具。

## 核心文件

- `MCPTool.ts` - 主工具实现（模板）
- `classifyForCollapse.ts` - 折叠分类
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 特性

- **动态模式** - MCP 工具在运行时动态添加
- **无固定模式** - 输入模式由 MCP 服务器定义
- **权限传递** - 权限检查传递到 MCP 服务器

## 对应命令/用途

MCPTool 是 MCP 集成的核心，允许 Claude Code 使用第三方工具。

**注意**：实际工具名称为 `mcp__serverName__toolName` 格式。
