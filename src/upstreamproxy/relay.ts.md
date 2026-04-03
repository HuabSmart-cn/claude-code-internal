# relay.ts - WebSocket CONNECT 中继

## 文件概述
**路径**: `src/upstreamproxy/relay.ts`
**功能**: 实现 CONNECT-over-WebSocket 中继器，允许 curl/gh/kubectl 等工具通过 WebSocket 隧道访问上游代理

---

## 核心概念
- **CONNECT 隧道**: HTTP CONNECT 方法建立到目标服务器的 TCP 隧道
- **WebSocket 传输**: 使用 WebSocket 封装二进制数据（因 CCR ingress 使用路径前缀路由）
- **Protobuf 编码**: 使用 `UpstreamProxyChunk` protobuf 格式封装数据
- **双运行时支持**: 同时支持 Bun 和 Node.js 运行时

## 关键类型/接口
```typescript
// WebSocket 类接口
type WebSocketLike = Pick<
  WebSocket,
  'onopen' | 'onmessage' | 'onerror' | 'onclose' | 'send' | 'close' | 'readyState' | 'binaryType'
>

// 连接状态
type ConnState = {
  ws?: WebSocketLike
  connectBuf: Buffer
  pinger?: ReturnType<typeof setInterval>
  pending: Buffer[]
  wsOpen: boolean
  established: boolean
  closed: boolean
}

// 客户端 socket 抽象
type ClientSocket = {
  write: (data: Uint8Array | string) => void
  end: () => void
}

// 中继器接口
type UpstreamProxyRelay = {
  port: number
  stop: () => void
}
```

## 核心函数

```typescript
/**
 * 编码 UpstreamProxyChunk protobuf 消息
 * message UpstreamProxyChunk { bytes data = 1; }
 */
export function encodeChunk(data: Uint8Array): Uint8Array

/**
 * 解码 UpstreamProxyChunk，返回 data 字段或 null
 */
export function decodeChunk(buf: Uint8Array): Uint8Array | null

/**
 * 启动中继器，返回绑定端口和停止函数
 */
export async function startUpstreamProxyRelay(opts: {
  wsUrl: string
  sessionId: string
  token: string
}): Promise<UpstreamProxyRelay>

/**
 * Bun 运行时中继实现
 */
function startBunRelay(
  wsUrl: string,
  authHeader: string,
  wsAuthHeader: string,
): UpstreamProxyRelay

/**
 * Node.js 运行时中继实现
 */
export async function startNodeRelay(
  wsUrl: string,
  authHeader: string,
  wsAuthHeader: string,
): Promise<UpstreamProxyRelay>
```

## 协议细节

### Protobuf 编码
- Tag = 0x0a (field 1, wire type 2)
- 后跟 varint 长度，再跟数据字节

### 心跳保活
- 30 秒间隔发送空 chunk（ping）
- Envoy 超时 50 秒，在其内留有安全余量

### 连接状态机
1. **Phase 1**: 积累 CONNECT 请求头（直到 CRLF CRLF）
2. **Phase 2**: WebSocket 存在但未 OPEN，缓冲数据
3. **Phase 3**: WS OPEN，转发缓冲数据，开心跳

## 中英对照
| English | 中文 |
|---------|------|
| CONNECT Relay | CONNECT 中继 |
| WebSocket Tunnel | WebSocket 隧道 |
| Upstream Proxy | 上游代理 |
| Chunk | 数据块 |
| Protobuf | Protocol Buffers |
| Connection State | 连接状态 |
| Handshake | 握手 |
| Keepalive | 保活 |
| Ping | 心跳 |
| Binary Type | 二进制类型 |
| Buffer | 缓冲区 |
| Established | 已建立 |
| Client Socket | 客户端 Socket |
