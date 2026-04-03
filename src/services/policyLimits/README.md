# services/policyLimits - 策略限制

## 功能

policyLimits 服务管理和执行各种使用策略和限制。

## 文件列表

| 文件 | 功能 |
|------|------|
| `index.ts` | 核心实现 (18KB) |
| `types.ts` | 类型定义 |

## 限制类型

### 1. API 速率限制
```typescript
interface RateLimit {
  requestsPerMinute: number
  tokensPerMinute: number
  burstSize: number
}
```

### 2. 使用配额
```typescript
interface Quota {
  monthlyTokenLimit: number
  dailyRequestLimit: number
  maxConcurrentRequests: number
}
```

### 3. 功能策略
```typescript
interface FeaturePolicy {
  autoCompact: boolean
  sessionMemory: boolean
  teamSync: boolean
  // ...
}
```

## 限制检查流程

```
请求
  ↓
policyLimits.check()
  ↓
是否超限?
  ├─ Yes → 拒绝/排队
  └─ No → 继续执行
```

## 响应头

API 调用会返回限制信息:
```
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 999
X-RateLimit-Reset: 1640000000
```
