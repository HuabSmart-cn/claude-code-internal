# sessionHistory.ts - 会话历史获取

## 文件概述
**路径**: `src/assistant/sessionHistory.ts`
**功能**: 提供会话历史事件的获取功能，支持分页加载最新的历史消息

---

## 核心概念
- **会话历史分页**: 通过 `anchor_to_latest` 和 `before_id` 游标实现双向分页
- **认证上下文**: 复用 OAuth 认证头和基础 URL，避免每次请求重新认证
- **SDKMessage**: 来自 Agent SDK 的标准消息格式，作为历史事件的数据结构

## 关键类型/接口
```typescript
// 分页结果类型
type HistoryPage = {
  /** 页面内按时间顺序排列的事件 */
  events: SDKMessage[]
  /** 当前页面中最旧事件的 ID，用于获取更早的页面 */
  firstId: string | null
  /** true = 还有更早的事件 */
  hasMore: boolean
}

// 认证上下文类型
type HistoryAuthCtx = {
  baseUrl: string
  headers: Record<string, string>
}
```

## 核心函数

```typescript
/**
 * 创建认证上下文，复用 OAuth token 和组织信息
 */
export async function createHistoryAuthCtx(
  sessionId: string,
): Promise<HistoryAuthCtx>

/**
 * 获取最新的 limit 条事件（按时间倒序）
 */
export async function fetchLatestEvents(
  ctx: HistoryAuthCtx,
  limit = HISTORY_PAGE_SIZE,
): Promise<HistoryPage | null>

/**
 * 获取 beforeId 之前的 events（更早的页面）
 */
export async function fetchOlderEvents(
  ctx: HistoryAuthCtx,
  beforeId: string,
  limit = HISTORY_PAGE_SIZE,
): Promise<HistoryPage | null>
```

## 中英对照
| English | 中文 |
|---------|------|
| Session History | 会话历史 |
| History Page | 历史页面 |
| Events | 事件 |
| Chronological order | 时间顺序 |
| Cursor | 游标 |
| Authentication Context | 认证上下文 |
| OAuth | OAuth 认证 |
| SDK Message | SDK 消息 |
| anchor_to_latest | 锚定到最新 |
| before_id | 之前 ID |
