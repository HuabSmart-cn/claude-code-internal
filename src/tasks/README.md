# tasks

## 功能
任务执行系统，支持多种类型的任务：本地 Shell、本地 Agent、远程 Agent、队友进程、Dream 等。

## 文件/子目录

### 核心文件
- `LocalMainSessionTask.ts` - 本地主会话任务 (15KB)
- `pillLabel.ts` - 任务标签
- `stopTask.ts` - 停止任务
- `types.ts` - 类型定义
- `LocalShellTask/` - 本地 Shell 任务
- `LocalAgentTask/` - 本地 Agent 任务
- `RemoteAgentTask/` - 远程 Agent 任务
- `InProcessTeammateTask/` - 进程内队友任务
- `DreamTask/` - Dream 任务

### LocalShellTask/ - 本地 Shell 任务
- `LocalShellTask.tsx` - Shell 任务实现 (66KB)
- `guards.ts` - 守卫条件
- `killShellTasks.ts` - 终止 Shell 任务

### LocalAgentTask/ - 本地 Agent 任务
- `LocalAgentTask.tsx` - 本地 Agent 实现 (82KB)

### RemoteAgentTask/ - 远程 Agent 任务
- `RemoteAgentTask.tsx` - 远程 Agent 实现 (126KB)

### InProcessTeammateTask/ - 进程内队友任务
- `InProcessTeammateTask.tsx` - 进程内队友 (16KB)
- `types.ts` - 类型定义

### DreamTask/ - Dream 任务
- `DreamTask.ts` - Dream 任务实现 (5KB)

## 核心概念

### 任务类型

| 类型 | 说明 |
|------|------|
| LocalShellTask | 在本地执行 Shell 命令 |
| LocalAgentTask | 在本地运行 Claude Agent |
| RemoteAgentTask | 连接远程 Agent 实例 |
| InProcessTeammateTask | 在同一进程内作为队友运行 |
| DreamTask | 创意/探索性任务 |

### 任务生命周期
1. **创建** - 实例化任务
2. **启动** - 开始执行
3. **运行** - 任务进行中
4. **停止** - 正常完成或被中断
5. **清理** - 资源回收

### 任务控制
- 启动/停止任务
- 任务状态查询
- 任务输出捕获
- 错误处理和重试
