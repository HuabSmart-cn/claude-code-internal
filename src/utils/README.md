# utils/ 目录概述

`utils/` 是 Claude Code 源码中最大的目录，包含约 290 个 TypeScript 文件和 32 个子目录。这个目录是应用程序的核心工具库，提供各种通用功能。

## 目录结构

```
utils/
├── 根目录文件 (约 270 个 .ts 文件)
├── background/           # 后台任务处理
├── bash/                 # Bash 命令执行
├── claudeInChrome/       # Chrome 扩展集成
├── computerUse/          # 计算机使用模式
├── deepLink/             # Deep Link 处理
├── dxt/                  # DXT 扩展
├── filePersistence/      # 文件持久化
├── git/                  # Git 集成
├── github/               # GitHub 集成
├── hooks/                # 钩子系统
├── mcp/                  # MCP (Model Context Protocol)
├── memory/               # 内存管理
├── messages/             # 消息处理
├── model/                # 模型管理
├── nativeInstaller/      # 原生安装程序
├── permissions/          # 权限管理
├── plugins/              # 插件系统
├── powershell/           # PowerShell 支持
├── processUserInput/     # 用户输入处理
├── sandbox/              # 沙箱执行
├── secureStorage/        # 安全存储
├── settings/             # 设置管理
├── shell/                # Shell 操作
├── skills/               # 技能系统
├── suggestions/          # 建议系统
├── swarm/                # Swarm 多代理
├── task/                 # 任务管理
├── telemetry/            # 遥测数据
├── teleport/             # 远程操作
├── todo/                 # Todo 功能
└── ultraplan/            # UltraPlan 功能
```

## 功能分类

### 核心配置与状态
- `config.ts` - 全局和项目配置管理
- `state.ts` - 应用程序状态管理
- `env.ts` / `envUtils.ts` - 环境变量处理

### 消息与 Token
- `messages.ts` - 消息创建和处理
- `tokens.ts` - Token 计算和统计
- `attachments.ts` - 附件处理

### Git 集成
- `git.ts` - Git 操作封装
- `git/` 子目录 - 更多 Git 功能

### 权限管理
- `permissions/` 目录 - 完整的权限系统
- `permissions.ts` - 权限检查和决策
- `classifierDecision.ts` - 分类器决策
- `yoloClassifier.ts` - YOLO 模式分类器

### Shell 与命令执行
- `bash/` 目录 - Bash 命令执行
- `shell/` 目录 - Shell 工具
- `powershell/` 目录 - PowerShell 支持

### 网络与 API
- `api.ts` - API 调用封装
- `auth.ts` - 认证管理
- `claudeDesktop.ts` - Claude Desktop 集成

### 文件操作
- `file.ts` - 文件操作
- `fsOperations.ts` - 文件系统操作
- `filePersistence/` - 文件持久化

### MCP (Model Context Protocol)
- `mcp/` 目录 - MCP 客户端和服务器
- `mcpUtils.ts` - MCP 工具函数

### 模型管理
- `model/` 目录 - 模型配置和选项
- `modelCost.ts` - 模型成本计算

### 工具函数
- `log.ts` - 日志记录
- `errors.ts` - 错误处理
- `json.ts` / `jsonRead.ts` / `slowOperations.ts` - JSON 处理
- `path.ts` - 路径操作
- `stringUtils.ts` - 字符串工具

### 安全相关
- `secureStorage/` - 安全存储
- `permissions/` - 权限管理
- `sandbox/` - 沙箱执行

## 重要文件详细解析

以下文件有独立的详细文档：
- [config.md](config.md) - 配置管理系统
- [messages.md](messages.md) - 消息处理系统
- [tokens.md](tokens.md) - Token 计算
- [git.md](git.md) - Git 集成
- [permissions/README.md](permissions/README.md) - 权限管理系统

## 子目录文档

每个子目录都有独立的 README.md 文档：
- [background/README.md](background/README.md)
- [bash/README.md](bash/README.md)
- [hooks/README.md](hooks/README.md)
- [model/README.md](model/README.md)
- [permissions/README.md](permissions/README.md)
- [shell/README.md](shell/README.md)
- [swarm/README.md](swarm/README.md)
- ... 等
