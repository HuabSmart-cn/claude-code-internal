# shared/ - 工具共享模块

## 功能

供多个工具共享的通用模块。

## 核心文件

| 文件 | 功能 |
|------|------|
| `spawnMultiAgent.ts` | 启动多代理（用于 AgentTool 和 TeamCreate） |
| `gitOperationTracking.ts` | Git 操作跟踪 |

## spawnMultiAgent.ts

提供 `spawnTeammate()` 函数，用于创建团队成员代理。

## gitOperationTracking.ts

跟踪 Git 操作，用于分析和工作流程。
