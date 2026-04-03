# claudeInChrome/ - Chrome 扩展集成

## 功能概述

`claudeInChrome/` 目录实现 Claude Code 与 Chrome 扩展的集成。

## 文件列表

```
claudeInChrome/
├── chromeNativeHost.ts   # Chrome 原生主机
├── common.ts           # 通用函数
├── mcpServer.ts       # MCP 服务器
├── prompt.ts          # 提示
├── setup.ts           # 设置
├── setupPortable.ts   # 便携设置
└── toolRendering.tsx  # 工具渲染
```

## 功能

### MCP 服务器
在 Chrome 扩展中运行 MCP 服务器。

### 工具渲染
在 Chrome 中渲染 Claude Code 工具。
