# hooks/toolPermission - 工具权限系统

## 功能

工具权限系统管理 Claude Code 中所有工具的调用权限，包括 Bash、文件操作、编辑等。

## 目录结构

```
toolPermission/
├── PermissionContext.ts       # 权限上下文管理
├── permissionLogging.ts      # 权限决策日志
└── handlers/                 # 权限处理程序
    ├── coordinatorHandler.ts     # 协调器处理
    ├── interactiveHandler.ts     # 交互式处理 (20KB)
    └── swarmWorkerHandler.ts     # Swarm Worker 处理
```

## 核心文件

### PermissionContext.ts
权限上下文工厂函数和队列操作接口。

### permissionLogging.ts
记录所有权限决策，用于审计和分析。

### handlers/
| 文件 | 功能 |
|------|------|
| `coordinatorHandler.ts` | 处理协调器发起的权限请求 |
| `interactiveHandler.ts` | 处理交互式权限确认对话框 |
| `swarmWorkerHandler.ts` | 处理 Swarm Worker 的权限请求 |

## 权限流程

1. **检查阶段** (`useCanUseTool.tsx`)
   - 检查工具是否配置为自动允许/拒绝
   - 运行分类器检查 (classifier)

2. **处理阶段** (handlers/)
   - `coordinatorHandler` - 自动化检查
   - `interactiveHandler` - 用户交互确认
   - `swarmWorkerHandler` - 子代理权限

3. **决策阶段**
   - 允许 (allow)
   - 拒绝 (deny)
   - 询问 (ask)

## 权限来源

| 来源 | 说明 |
|------|------|
| `hook` | 通过 hook 配置的权限 |
| `user` | 用户手动确认/拒绝 |
| `classifier` | 自动分类器判断 |
| `config` | 配置文件设置 |
