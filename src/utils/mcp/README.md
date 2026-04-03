# mcp/ - MCP (Model Context Protocol)

## 功能概述

`mcp/` 目录实现 MCP 客户端功能，允许 Claude Code 与外部工具和服务集成。

## 文件列表

```
mcp/
├── (多个 MCP 相关文件)
```

## MCP 协议

MCP 是一种标准协议，允许 AI 模型与外部工具和服务通信。

## 核心功能

### MCP 客户端
连接到 MCP 服务器并执行工具调用。

### 服务器配置
```typescript
interface McpServerConfig {
  command: string
  args: string[]
  env?: Record<string, string>
}
```

## 使用场景

- 文件系统操作
- Git 操作
- 数据库连接
- API 调用
- 自定义工具集成
