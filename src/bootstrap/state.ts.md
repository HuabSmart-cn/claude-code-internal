# state.ts - 全局状态管理

## 文件概述
**路径**: `src/bootstrap/state.ts`
**功能**: 管理 Claude Code 运行时的全局状态，包括会话信息、遥测数据、模型使用统计等

---

## 核心概念
- **单例状态**: 通过 `STATE` 全局对象管理所有会话级别状态
- **状态访问器模式**: 每个状态字段都有对应的 getter/setter 函数
- **会话管理**: 支持会话 ID 生成、切换、父会话追踪
- **遥测集成**: 与 OpenTelemetry 集成，记录 meter、logger、tracer

## 关键类型/接口
```typescript
// 通道条目类型
type ChannelEntry =
  | { kind: 'plugin'; name: string; marketplace: string; dev?: boolean }
  | { kind: 'server'; name: string; dev?: boolean }

// 归因计数器
type AttributedCounter = {
  add(value: number, additionalAttributes?: Attributes): void
}

// 会话 Cron 任务
type SessionCronTask = {
  id: string
  cron: string
  prompt: string
  createdAt: number
  recurring?: boolean
  agentId?: string
}

// 调用技能信息
type InvokedSkillInfo = {
  skillName: string
  skillPath: string
  content: string
  invokedAt: number
  agentId: string | null
}
```

## 核心函数

### 会话管理
```typescript
export function getSessionId(): SessionId
export function regenerateSessionId(options?: { setCurrentAsParent?: boolean }): SessionId
export function getParentSessionId(): SessionId | undefined
export function switchSession(sessionId: SessionId, projectDir?: string | null): void
export const onSessionSwitch: (callback: (id: SessionId) => void) => void
```

### 目录管理
```typescript
export function getOriginalCwd(): string
export function getProjectRoot(): string
export function setOriginalCwd(cwd: string): void
export function setProjectRoot(cwd: string): void
export function getCwdState(): string
export function setCwdState(cwd: string): void
```

### 成本与使用统计
```typescript
export function addToTotalCostState(cost: number, modelUsage: ModelUsage, model: string): void
export function getTotalCostUSD(): number
export function getTotalInputTokens(): number
export function getTotalOutputTokens(): number
export function getModelUsage(): { [modelName: string]: ModelUsage }
```

### 交互时间追踪
```typescript
export function updateLastInteractionTime(immediate?: boolean): void
export function flushInteractionTime(): void
export function getLastInteractionTime(): number
```

### 滚动抑制（Scroll Drain Suspension）
```typescript
export function markScrollActivity(): void
export function getIsScrollDraining(): boolean
export async function waitForScrollIdle(): Promise<void>
```

### Hooks 注册
```typescript
export function registerHookCallbacks(
  hooks: Partial<Record<HookEvent, RegisteredHookMatcher[]>>,
): void
export function getRegisteredHooks(): Partial<Record<HookEvent, RegisteredHookMatcher[]>> | null
```

### 技能追踪
```typescript
export function addInvokedSkill(
  skillName: string,
  skillPath: string,
  content: string,
  agentId?: string | null,
): void
export function getInvokedSkills(): Map<string, InvokedSkillInfo>
```

## 中英对照
| English | 中文 |
|---------|------|
| Global State | 全局状态 |
| Session ID | 会话 ID |
| Parent Session | 父会话 |
| Project Root | 项目根目录 |
| Working Directory | 工作目录 |
| Telemetry | 遥测 |
| Meter | 计量器 |
| Cost Tracking | 成本追踪 |
| Token Usage | Token 使用量 |
| Scroll Drain | 滚动排空 |
| Hooks | 钩子 |
| Invoked Skills | 调用的技能 |
| Beta Header Latch | Beta 头信息闩锁 |
| Prompt Cache | 提示缓存 |
