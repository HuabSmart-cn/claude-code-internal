# services/api - API 调用层

## 功能

API 层负责与 Claude API 通信，处理认证、请求重试、错误处理和日志记录。

## 文件列表

| 文件 | 功能 | 大小 |
|------|------|------|
| `claude.ts` | Claude API 核心调用 | 125KB |
| `client.ts` | API 客户端封装 | 161KB |
| `errors.ts` | API 错误类型定义 | 41KB |
| `withRetry.ts` | 重试逻辑 | 28KB |
| `grove.ts` | Grove API 集成 | 11KB |
| `logging.ts` | API 请求日志 | 24KB |
| `filesApi.ts` | 文件相关 API | 21KB |
| `sessionIngress.ts` | 会话入口管理 | 17KB |
| `errorUtils.ts` | 错误工具函数 | 8KB |
| `dumpPrompts.ts` | Prompt 转储 | 7KB |
| `referral.ts` | 推荐系统 | 7KB |
| `promptCacheBreakDetection.ts` | Prompt 缓存检测 | 26KB |
| `bootstrap.ts` | 启动初始化 | 4KB |
| `adminRequests.ts` | 管理请求 | 3KB |
| `emptyUsage.ts` | 空使用记录 | 712B |
| `firstTokenDate.ts` | 首 token 时间 | 1KB |
| `metricsOptOut.ts` | 指标退出 | 5KB |
| `overageCreditGrant.ts` | 超额信用授予 | 4KB |
| `ultrareviewQuota.ts` | UltraReview 配额 | 1KB |
| `usage.ts` | 使用量跟踪 | 1KB |

## 核心模块

### claude.ts
Claude Messages API 的主要封装，包含:
- 消息创建和发送
- Token 计算
- 上下文管理

### client.ts
HTTP 客户端封装，处理:
- 请求/响应拦截
- 超时配置
- 重试逻辑

### errors.ts
完整的错误类型体系:
- `APIError` - API 错误基类
- `RateLimitError` - 速率限制
- `AuthenticationError` - 认证错误
- `ValidationError` - 验证错误

### withRetry.ts
智能重试机制:
- 指数退避
- 速率限制处理
- 最大重试次数

## 使用方式

```typescript
import { ClaudeAPI } from './services/api/claude.ts'

const api = new ClaudeAPI({
  apiKey: process.env.ANTHROPIC_API_KEY,
})

const response = await api.createMessage({
  model: 'claude-3-5-sonnet-20241022',
  max_tokens: 1024,
  messages: [{ role: 'user', content: 'Hello' }]
})
```
