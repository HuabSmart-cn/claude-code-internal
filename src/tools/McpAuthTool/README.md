# McpAuthTool

## 功能

为需要 OAuth 认证的 MCP 服务器启动认证流程。

## 核心文件

- `McpAuthTool.ts` - 主工具实现

## 工作原理

当 MCP 服务器需要认证时，创建伪工具（pseudo-tool）来：
1. 启动 OAuth 流程
2. 返回授权 URL
3. 用户完成认证后，真实工具自动可用

## 对应命令/用途

McpAuthTool 用于处理 MCP 服务器的 OAuth 认证流程。

**注意**：这是一个动态创建的工具，不是静态注册的。
