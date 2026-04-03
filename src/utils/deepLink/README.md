# deepLink/ - Deep Link 处理

## 功能概述

`deepLink/` 目录处理 Deep Link 协议，允许通过 URL 启动 Claude Code。

## 文件列表

```
deepLink/
├── banner.ts            # 横幅
├── parseDeepLink.ts   # 解析 Deep Link
├── protocolHandler.ts  # 协议处理器
├── registerProtocol.ts # 注册协议
├── terminalLauncher.ts # 终端启动器
└── terminalPreference.ts  # 终端偏好
```

## Deep Link 格式

```
claude://...
```

## 协议处理

`registerProtocol.ts` - 注册 `claude://` 协议处理器。
