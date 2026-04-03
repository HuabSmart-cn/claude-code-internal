# coordinatorMode.ts - 协调者模式

## 文件概述
**路径**: `src/coordinator/coordinatorMode.ts`
**功能**: 实现协调者模式，使 Claude Code 能够编排多个 Worker 子代理完成任务

---

## 核心概念
- **协调者（Coordinator）**: 主控代理，负责分解任务、指派工作给 Worker、汇总结果
- **Worker**: 被协调者spawn 的子代理，执行具体的研究、实现和验证任务
- **任务通知（Task Notification）**: Worker 完成时通过 XML 格式通知协调者
- **并发执行**: 协调者可以并行启动多个 Worker 加速任务完成
- **简单模式（Simple Mode）**: 通过 `CLAUDE_CODE_SIMPLE` 环境变量限制 Worker 工具集

## 关键类型/接口
```typescript
// 协调者用户上下文
type CoordinatorUserContext = {
  workerToolsContext: string  // Worker 可用工具列表
}

// 协调者系统提示
type CoordinatorSystemPrompt = string
```

## 核心函数

```typescript
/**
 * 检查当前是否处于协调者模式
 */
export function isCoordinatorMode(): boolean

/**
 * 检查会话存储的模式是否与当前模式匹配
 * 如不匹配则切换环境变量并返回警告消息
 */
export function matchSessionMode(
  sessionMode: 'coordinator' | 'normal' | undefined,
): string | undefined

/**
 * 获取协调者用户上下文（Worker 工具列表等）
 */
export function getCoordinatorUserContext(
  mcpClients: ReadonlyArray<{ name: string }>,
  scratchpadDir?: string,
): { [k: string]: string }

/**
 * 获取协调者系统提示（完整的提示词模板）
 */
export function getCoordinatorSystemPrompt(): string
```

## 协调者工作流程

### 1. 任务分解
| 阶段 | 执行者 | 目的 |
|------|--------|------|
| Research | Workers（并行） | 调研代码库、理解问题 |
| Synthesis | 协调者 | 阅读发现、综合分析、制定实现规范 |
| Implementation | Workers | 按规范实施变更、提交 |
| Verification | Workers | 测试验证变更是否有效 |

### 2. 工具使用
- **AgentTool**: spawn 新 Worker
- **SendMessageTool**: 继续已有 Worker
- **TaskStopTool**: 停止运行中的 Worker

### 3. 任务通知格式
```xml
<task-notification>
<task-id>{agentId}</task-id>
<status>completed|failed|killed</status>
<summary>{状态摘要}</summary>
<result>{Agent 最终文本响应}</result>
<usage>
  <total_tokens>N</total_tokens>
  <tool_uses>N</tool_uses>
  <duration_ms>N</duration_ms>
</usage>
</task-notification>
```

## 中英对照
| English | 中文 |
|---------|------|
| Coordinator Mode | 协调者模式 |
| Worker | 工作代理 |
| Task Notification | 任务通知 |
| Subagent | 子代理 |
| Task Workflow | 任务工作流 |
| Research | 研究调研 |
| Synthesis | 综合分析 |
| Implementation | 实施实现 |
| Verification | 验证 |
| Parallelism | 并行执行 |
| Concurrency | 并发性 |
| SendMessage | 发送消息 |
| Task Stop | 任务停止 |
