# cost-tracker.ts

## 文件概述
**路径**: `src/cost-tracker.ts`
**功能**: 追踪和管理 API 使用成本、会话时长和代码变更统计
**重要程度**: ★★★★☆

---

## 核心概念
### 成本追踪
追踪 Claude Code 会话中的：
- 总成本（USD）
- API 调用时长
- 代码变更行数（新增/删除）
- Token 使用量（输入/输出/缓存读取/缓存创建）
- Web 搜索请求数

### 模型使用统计
按模型名称聚合的使用数据。

---

## 主要类型/接口
```typescript
type ModelUsage = {
  inputTokens: number
  outputTokens: number
  cacheReadInputTokens: number
  cacheCreationInputTokens: number
  webSearchRequests: number
  costUSD: number
  contextWindow: number
  maxOutputTokens: number
}

type StoredCostState = {
  totalCostUSD: number
  totalAPIDuration: number
  totalAPIDurationWithoutRetries: number
  totalToolDuration: number
  totalLinesAdded: number
  totalLinesRemoved: number
  lastDuration: number | undefined
  modelUsage: { [modelName: string]: ModelUsage } | undefined
}
```

---

## 关键函数
```typescript
/**
 * 添加到会话总成本
 */
function addToTotalSessionCost(cost: number, usage: Usage, model: string): number

/**
 * 获取当前总成本
 */
function getTotalCostUSD(): number

/**
 * 格式化总成本输出
 */
function formatTotalCost(): string

/**
 * 获取存储的会话成本（用于恢复）
 */
function getStoredSessionCosts(sessionId: string): StoredCostState | undefined

/**
 * 恢复会话成本状态
 */
function restoreCostStateForSession(sessionId: string): boolean

/**
 * 保存当前会话成本到项目配置
 */
function saveCurrentSessionCosts(fpsMetrics?: FpsMetrics): void
```

---

## 与其他模块的关系
- 调用：
  - `bootstrap/state.js` - 状态管理
  - `utils/config.js` - 项目配置
  - `utils/modelCost.js` - 成本计算
- 被调用：
  - `costHook.ts` - React hook
  - `main.tsx` - 启动时恢复成本
  - `setup.ts` - 保存上次会话成本

---

## 英文对照词汇表
| English | 中文 |
|---------|------|
| Cost tracker | 成本追踪 |
| Token | Token |
| Input tokens | 输入 Token |
| Output tokens | 输出 Token |
| Cache read | 缓存读取 |
| Cache creation | 缓存创建 |
| Web search | 网络搜索 |
| Duration | 时长 |
| Lines added | 新增行数 |
| Lines removed | 删除行数 |
