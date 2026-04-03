# swarm/ - Swarm 多代理系统

## 功能概述

`swarm/` 目录实现 Swarm 多代理架构，允许创建和管理多个协作的 AI 代理。

## 文件列表

```
swarm/
├── backends/              # 后端实现
├── constants.ts           # 常量
├── inProcessRunner.ts     # 进程内运行器
├── It2SetupPrompt.tsx     # iTerm2 设置提示
├── leaderPermissionBridge.ts  # 领导者权限桥接
├── permissionSync.ts      # 权限同步
├── reconnection.ts         # 重连
├── spawnInProcess.ts      # 进程内生成
├── spawnUtils.ts          # 生成工具
├── teamHelpers.ts         # 团队辅助
├── teammateInit.ts        # 队友初始化
├── teammateLayoutManager.ts # 布局管理
├── teammateModel.ts       # 队友模型
├── teammatePromptAddendum.ts  # 提示附录
└── reconnection.ts        # 重连逻辑
```

## 核心概念

### Leader Agent
主代理，协调其他代理的工作。

### Teammate Agents
队友代理，执行特定任务。

### Swarm 模式
允许多个代理并行工作，共享上下文。

## 进程内运行

`inProcessRunner.ts` 允许在当前进程内运行代理，而不是生成子进程。

## 权限同步

`permissionSync.ts` 在主代理和队友代理之间同步权限设置。
