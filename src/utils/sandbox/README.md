# sandbox/ - 沙箱执行

## 功能概述

`sandbox/` 目录提供命令的沙箱执行环境，防止恶意操作。

## 文件列表

```
sandbox/
├── sandbox-adapter.ts    # 沙箱适配器
└── sandbox-ui-utils.ts   # UI 工具
```

## 核心功能

### 沙箱适配器
`sandbox-adapter.ts` - 适配不同的沙箱实现。

## 用途

- 限制文件系统访问
- 网络访问控制
- 进程隔离
