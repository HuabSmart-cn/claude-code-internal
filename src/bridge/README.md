# bridge

## 功能
桥接模式实现，用于远程协作场景，支持远程会话管理、消息传递和权限控制。

## 文件说明

- `bridgeApi.ts` - 桥接 API
- `bridgeConfig.ts` - 桥接配置
- `bridgeDebug.ts` - 调试工具
- `bridgeEnabled.ts` - 启用状态检查
- `bridgeMain.ts` - 桥接主逻辑 (115KB)
- `bridgeMessaging.ts` - 消息传递
- `bridgePermissionCallbacks.ts` - 权限回调
- `bridgePointer.ts` - 指针管理
- `bridgeStatusUtil.ts` - 状态工具
- `bridgeUI.ts` - 桥接 UI
- `capacityWake.ts` - 容量唤醒
- `codeSessionApi.ts` - 代码会话 API
- `createSession.ts` - 会话创建
- `debugUtils.ts` - 调试工具
- `envLessBridgeConfig.ts` - 无环境配置
- `flushGate.ts` - 刷新门控
- `inboundAttachments.ts` - 附件处理
- `inboundMessages.ts` - 入站消息
- `initReplBridge.ts` - REPL 桥接初始化
- `jwtUtils.ts` - JWT 工具
- `pollConfig.ts` - 轮询配置
- `pollConfigDefaults.ts` - 轮询默认配置
- `remoteBridgeCore.ts` - 远程桥接核心 (39KB)
- `replBridge.ts` - REPL 桥接 (100KB)
- `replBridgeHandle.ts` - REPL 句柄
- `replBridgeTransport.ts` - 传输层
- `sessionIdCompat.ts` - 会话 ID 兼容
- `sessionRunner.ts` - 会话运行
- `trustedDevice.ts` - 信任设备
- `types.ts` - 类型定义
- `workSecret.ts` - 工作密钥

## 核心概念

### 远程桥接
通过桥接模式实现本地 Claude Code 与远程实例的通信。

### 会话管理
- 创建远程会话
- 会话生命周期管理
- 会话 ID 兼容性处理

### 消息传递
- 入站/出站消息处理
- 附件管理
- 消息编解码

### 权限控制
- 桥接权限回调
- 信任设备验证
- 工作密钥管理

### 传输层
- REPL 桥接传输
- WebSocket 传输
- HTTP 轮询传输
