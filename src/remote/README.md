# remote

## 功能
远程会话管理模块，支持 WebSocket 远程连接和会话控制。

## 文件说明

- `remotePermissionBridge.ts` - 远程权限桥接
- `RemoteSessionManager.ts` - 远程会话管理器 (9KB)
- `sdkMessageAdapter.ts` - SDK 消息适配器 (9KB)
- `SessionsWebSocket.ts` - WebSocket 会话 (12KB)

## 核心概念

### 远程会话
- 创建直接连接会话
- 会话生命周期管理
- 多会话并发管理

### WebSocket 通信
- 实时双向通信
- 自动重连
- 心跳保活

### 权限桥接
远程会话的权限检查和委托。

### 消息适配
SDK 消息格式与内部消息格式的转换。
