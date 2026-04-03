# tokenBudget.ts - Token 预算管理

## 文件概述
**路径**: `src/query/tokenBudget.ts`
**功能**: 管理对话的 Token 使用预算

---

## 核心概念
- **Token 预算**: 控制单轮和整体对话的 token 消耗
- **预算追踪**: 记录已使用的 token 数量
- **预算检查**: 确保不超过预算限制

---

## 主要功能
```typescript
/**
 * 创建预算追踪器
 */
createBudgetTracker()

/**
 * 检查是否在预算内
 */
checkTokenBudget(tracker, usage)

/**
 * 获取当前轮次的 token 预算
 */
getCurrentTurnTokenBudget()
```

---

## 英文对照

| English | 中文 |
|---------|------|
| Token Budget | Token 预算 |
| Budget Tracker | 预算追踪器 |
| Turn Budget | 单轮预算 |
| Usage | 使用量 |
