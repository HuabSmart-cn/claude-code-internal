# tasks.ts

## 文件概述
**路径**: `src/tasks.ts`
**功能**: 任务管理入口，提供任务类型到任务实例的映射
**重要程度**: ★★★★☆

---

## 核心概念
### 任务类型
参见 `Task.ts` 中的 TaskType 定义。

### 任务实现
- `LocalShellTask`: 本地 Shell 任务
- `LocalAgentTask`: 本地 Agent 任务
- `RemoteAgentTask`: 远程 Agent 任务
- `DreamTask`: 梦境任务
- `LocalWorkflowTask`: 本地工作流任务 (可选)
- `MonitorMcpTask`: MCP 监控任务 (可选)

---

## 关键函数
```typescript
/**
 * 获取所有任务实例
 */
function getAllTasks(): Task[]

/**
 * 根据类型获取任务实例
 */
function getTaskByType(type: TaskType): Task | undefined
```

---

## 实现
```typescript
export function getAllTasks(): Task[] {
  const tasks: Task[] = [
    LocalShellTask,
    LocalAgentTask,
    RemoteAgentTask,
    DreamTask,
  ]
  if (LocalWorkflowTask) tasks.push(LocalWorkflowTask)
  if (MonitorMcpTask) tasks.push(MonitorMcpTask)
  return tasks
}

export function getTaskByType(type: TaskType): Task | undefined {
  return getAllTasks().find(t => t.type === type)
}
```

---

## 与其他模块的关系
- 调用：各种任务实现类
  - `tasks/LocalShellTask/`
  - `tasks/LocalAgentTask/`
  - `tasks/RemoteAgentTask/`
  - `tasks/DreamTask/`
- 被调用：
  - `Task.ts` - 类型定义
  - 任务执行相关模块

---

## 英文对照词汇表
| English | 中文 |
|---------|------|
| Task | 任务 |
| Local shell | 本地 Shell |
| Local agent | 本地代理 |
| Remote agent | 远程代理 |
| Workflow | 工作流 |
| Monitor | 监控 |
