# nativeInstaller/ - 原生安装程序

## 功能概述

`nativeInstaller/` 目录处理 Claude Code 的原生安装程序功能。

## 文件列表

```
nativeInstaller/
├── download.ts       # 下载
├── index.ts         # 入口
├── installer.ts     # 安装程序 (54KB)
├── packageManagers.ts  # 包管理器
└── pidLock.ts      # PID 锁
```

## 功能

### 安装
`installer.ts` - 原生安装逻辑。

### 下载
`download.ts` - 下载安装包。

### 包管理器
`packageManagers.ts` - 支持多种包管理器。
