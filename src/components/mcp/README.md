# mcp/

## 功能
MCP (Model Context Protocol) 服务器管理 UI，负责 MCP 服务器的连接、配置、工具浏览和状态管理。

## 组件列表

### 核心组件
- `MCPListPanel.tsx` - MCP 服务器列表面板（58KB）
- `MCPSettings.tsx` - MCP 设置界面（40KB）
- `MCPRemoteServerMenu.tsx` - 远程服务器菜单（102KB）
- `MCPAgentServerMenu.tsx` - Agent 服务器菜单（26KB）
- `MCPStdioServerMenu.tsx` - Stdio 服务器菜单（28KB）
- `MCPToolListView.tsx` - MCP 工具列表视图
- `MCPToolDetailView.tsx` - MCP 工具详情视图
- `MCPReconnect.tsx` - 重连组件
- `McpParsingWarnings.tsx` - 解析警告

### 工具函数
- `utils/reconnectHelpers.tsx` - 重连辅助函数

## 重要组件

### MCPListPanel
MCP 服务器列表管理界面，提供：
- 已配置服务器的列表
- 添加/移除服务器
- 查看服务器状态
- 快速连接/断开

### MCPRemoteServerMenu
远程 MCP 服务器配置界面，用于：
- 配置远程 MCP 服务器 URL
- 设置认证信息
- 管理服务器连接

### MCPToolListView / MCPToolDetailView
MCP 工具浏览界面：
- 列出服务器提供的所有工具
- 查看工具的参数和描述
- 了解工具用途

### MCPReconnect
处理 MCP 连接失败后的重连逻辑。
