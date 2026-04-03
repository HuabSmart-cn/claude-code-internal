# computerUse/ - 计算机使用模式

## 功能概述

`computerUse/` 目录实现 Claude 的计算机使用模式，允许 AI 直接控制计算机。

## 文件列表

```
computerUse/
├── appNames.ts            # 应用名称
├── cleanup.ts           # 清理
├── common.ts           # 通用函数
├── computerUseLock.ts  # 计算机锁
├── drainRunLoop.ts    # 耗尽运行循环
├── escHotkey.ts       # ESC 热键
├── executor.ts        # 执行器
├── gates.ts           # 门控
├── hostAdapter.ts     # 主机适配器
├── inputLoader.ts     # 输入加载
├── mcpServer.ts       # MCP 服务器
├── setup.ts           # 设置
├── swiftLoader.ts     # Swift 加载器
├── toolRendering.tsx  # 工具渲染
└── wrapper.tsx       # 包装器
```

## 功能

### 视觉元素检测
检测屏幕上的 UI 元素。

### 鼠标/键盘控制
模拟用户输入。

### MCP 服务器
提供 MCP 接口控制计算机。
