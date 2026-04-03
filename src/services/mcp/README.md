# services/mcp - MCP 协议实现

## 功能

MCP (Model Context Protocol) 服务负责与外部 MCP 服务器通信，提供扩展的工具和资源访问。

## 文件列表

| 文件 | 功能 | 大小 |
|------|------|------|
| `client.ts` | MCP 客户端核心 | 118KB |
| `auth.ts` | MCP 认证处理 | 88KB |
| `config.ts` | MCP 配置管理 | 51KB |
| `useManageMCPConnections.ts` | 连接生命周期管理 | 44KB |
| `xaa.ts` | XAA 集成 | 18KB |
| `channelPermissions.ts` | 渠道权限 | 8KB |
| `channelNotification.ts` | 渠道通知 | 12KB |
| `elicitationHandler.ts` | 用户征询处理 | 10KB |
| `utils.ts` | 工具函数 | 17KB |
| `types.ts` | 类型定义 | 6KB |
| `claudeai.ts` | Claude.ai 集成 | 6KB |
| `headersHelper.ts` | HTTP 头帮助 | 4KB |
| `oauthPort.ts` | OAuth 端口 | 2KB |
| `officialRegistry.ts` | 官方注册表 | 2KB |
| `SdkControlTransport.ts` | SDK 控制传输 | 4KB |
| `InProcessTransport.ts` | 进程内传输 | 1KB |
| `mcpStringUtils.ts` | 字符串工具 | 3KB |
| `normalization.ts` | 标准化 | 879B |
| `vscodeSdkMcp.ts` | VSCode SDK MCP | 3KB |
| `xaaIdpLogin.ts` | XAA IDP 登录 | 16KB |

## MCP 连接类型

### 1. STDIO 连接
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/tmp"]
    }
  }
}
```

### 2. StreamableHTTP 连接
```json
{
  "mcpServers": {
    "api": {
      "url": "https://api.example.com/mcp"
    }
  }
}
```

### 3. SSE 连接
Server-Sent Events 传输。

## 核心功能

### 工具发现
```typescript
const tools = await client.listTools()
// [{ name: "read_file", description: "...", inputSchema: {...} }]
```

### 工具调用
```typescript
const result = await client.callTool({
  name: "read_file",
  arguments: { path: "/tmp/test.txt" }
})
```

### 资源管理
```typescript
const resources = await client.listResources()
const resource = await client.readResource("file:///tmp/data.json")
```

## 认证

MCP 支持多种认证方式:
- OAuth 2.0
- API Key
- Bearer Token

## 连接管理

```typescript
// useManageMCPConnections.ts
const {
  connections,     // 当前连接列表
  connect,         // 建立连接
  disconnect,      // 断开连接
  reconnect,       // 重新连接
  getConnectionStatus  // 获取状态
} = useManageMCPConnections()
```
