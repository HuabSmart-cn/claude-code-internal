# cli

## 功能
命令行接口模块，负责 CLI 输出、传输层和命令处理。

## 文件/子目录

### 核心文件
- `exit.ts` - 退出处理
- `ndjsonSafeStringify.ts` - NDJSON 安全序列化
- `print.ts` - 打印输出 (212KB)
- `remoteIO.ts` - 远程 IO
- `structuredIO.ts` - 结构化 IO (28KB)
- `update.ts` - 更新相关
- `handlers/` - 命令处理器
- `transports/` - 传输层

### cli/handlers/ - 命令处理器
- `agents.ts` - Agent 处理
- `auth.ts` - 认证处理
- `autoMode.ts` - 自动模式
- `mcp.tsx` - MCP 处理器 (56KB)
- `plugins.tsx` - 插件处理 (31KB)
- `util.tsx` - 工具函数

### cli/transports/ - 传输层
- `ccrClient.ts` - CCR 客户端 (33KB)
- `HybridTransport.ts` - 混合传输
- `SerialBatchEventUploader.ts` - 批量事件上传
- `SSETransport.ts` - Server-Sent Events 传输
- `transportUtils.ts` - 传输工具
- `WebSocketTransport.ts` - WebSocket 传输
- `WorkerStateUploader.ts` - Worker 状态上传

## 核心概念

### 传输层
- **WebSocketTransport**: WebSocket 长连接
- **SSETransport**: Server-Sent Events 单向流
- **HybridTransport**: 混合模式传输

### 结构化 IO
支持结构化的命令行输出，便于程序化解析。

### 事件上传
- 批量事件上传
- Worker 状态同步
- CCR 客户端通信

### 命令处理
- Auth 认证流程
- MCP 协议处理
- 插件管理
