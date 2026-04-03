# Task.ts

## 文件概述
**路径**: `src/Task.ts`
**功能**: 定义任务类型、状态管理和任务ID生成机制
**重要程度**: ★★★★☆

---

## 核心概念
### TaskType (任务类型)
Claude Code 中支持的任务类型枚举：
- `local_bash`: 本地 Bash 任务
- `local_agent`: 本地 Agent 任务
- `remote_agent`: 远程 Agent 任务
- `in_process_teammate`: 进程内队友
- `local_workflow`: 本地工作流
- `monitor_mcp`: MCP 监控任务
- `dream`: 梦境任务

### TaskStatus (任务状态)
- `pending`: 等待中
- `running`: 运行中
- `completed`: 已完成
- `failed`: 失败
- `killed`: 被终止

### isTerminalTaskStatus
判断任务是否处于终态（completed/failed/killed），用于防止向已死亡的任务注入消息。

---

## 主要类型/接口
```typescript
// 任务ID前缀映射
type TaskIdPrefix = 'b' | 'a' | 'r' | 't' | 'w' | 'm' | 'd'

// 任务句柄
type TaskHandle = {
  taskId: string
  cleanup?: () => void
}

// 任务上下文
type TaskContext = {
  abortController: AbortController
  getAppState: () => AppState
  setAppState: SetAppState
}

// 任务状态基类
type TaskStateBase = {
  id: string
  type: TaskType
  status: TaskStatus
  description: string
  toolUseId?: string
  startTime: number
  endTime?: number
  totalPausedMs?: number
  outputFile: string
  outputOffset: number
  notified: boolean
}

// 本地 Shell 任务输入
type LocalShellSpawnInput = {
  command: string
  description: string
  timeout?: number
  toolUseId?: string
  agentId?: AgentId
  kind?: 'bash' | 'monitor'
}

// 任务接口
type Task = {
  name: string
  type: TaskType
  kill(taskId: string, setAppState: SetAppState): Promise<void>
}
```

---

## 关键函数
```typescript
/**
 * 生成唯一任务ID
 * 格式: 前缀 + 8位随机字符 (36^8 ≈ 2.8万亿组合)
 */
function generateTaskId(type: TaskType): string

/**
 * 创建任务状态基对象
 */
function createTaskStateBase(
  id: string,
  type: TaskType,
  description: string,
  toolUseId?: string
): TaskStateBase

/**
 * 判断任务状态是否为终态
 */
function isTerminalTaskStatus(status: TaskStatus): boolean
```

---

## 与其他模块的关系
- 调用：`getTaskOutputPath` (utils/task/diskOutput.js) - 获取任务输出文件路径
- 被调用：`tasks.ts` - 获取所有任务实例

---

## 英文对照词汇表
| English | 中文 |
|---------|------|
| Task | 任务 |
| TaskType | 任务类型 |
| TaskStatus | 任务状态 |
| TaskHandle | 任务句柄 |
| TaskContext | 任务上下文 |
| TaskStateBase | 任务状态基类 |
| LocalShellSpawnInput | 本地Shell输入 |
| Terminal state | 终态 |
