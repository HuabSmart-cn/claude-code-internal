# QueryEngine.ts

## 文件概述
**路径**: `src/QueryEngine.ts`
**功能**: SDK/Headless 模式的查询引擎，提供与 `query.ts` 相似的功能但用于编程式调用
**重要程度**: ★★★★★

---

## 核心概念
### QueryEngine
拥有查询生命周期和会话状态的类，用于：
- Headless/SDK 模式
- 未来可能用于 REPL

### 查询会话
每个 `QueryEngine` 实例对应一个会话，包含：
- 消息历史
- 文件缓存
- 使用统计
- 权限拒绝追踪

---

## 主要类型/接口
```typescript
type QueryEngineConfig = {
  cwd: string
  tools: Tools
  commands: Command[]
  mcpClients: MCPServerConnection[]
  agents: AgentDefinition[]
  canUseTool: CanUseToolFn
  getAppState: () => AppState
  setAppState: (f: (prev: AppState) => AppState) => void
  initialMessages?: Message[]
  readFileCache: FileStateCache
  customSystemPrompt?: string
  appendSystemPrompt?: string
  userSpecifiedModel?: string
  fallbackModel?: string
  thinkingConfig?: ThinkingConfig
  maxTurns?: number
  maxBudgetUsd?: number
  taskBudget?: { total: number }
  // ... 更多选项
}
```

---

## QueryEngine 类
```typescript
class QueryEngine {
  constructor(config: QueryEngineConfig)

  /**
   * 提交消息并生成响应
   * AsyncGenerator<SDKMessage> - 产出各种消息类型
   */
  async *submitMessage(
    prompt: string | ContentBlockParam[],
    options?: { uuid?: string; isMeta?: boolean }
  ): AsyncGenerator<SDKMessage, void, unknown>

  interrupt(): void
  getMessages(): readonly Message[]
  getReadFileState(): FileStateCache
  getSessionId(): string
  setModel(model: string): void
}
```

---

## ask() 便捷函数
单次查询的便捷包装器：
```typescript
async function* ask({
  commands,
  prompt,
  cwd,
  tools,
  // ...
}): AsyncGenerator<SDKMessage, void, unknown>
```

---

## 与其他模块的关系
- 调用：
  - `query.ts` - 核心查询逻辑
  - `hooks/useCanUseTool.ts` - 权限检查
  - `utils/processUserInput/processUserInput.js` - 用户输入处理
- 被调用：
  - SDK 入口
  - Headless 模式

---

## 英文对照词汇表
| English | 中文 |
|---------|------|
| Query engine | 查询引擎 |
| SDK | 软件开发工具包 |
| Headless | 无头模式 |
| Session | 会话 |
| Submit | 提交 |
| Interrupt | 中断 |
