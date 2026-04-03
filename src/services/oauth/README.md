# services/oauth - OAuth 认证

## 功能

OAuth 服务处理第三方服务的认证授权，如 Claude.ai API 访问。

## 文件列表

| 文件 | 功能 |
|------|------|
| `client.ts` | OAuth 客户端 |
| `auth-code-listener.ts` | 授权码监听 |
| `index.ts` | 入口文件 |
| `getOauthProfile.ts` | 获取用户信息 |
| `crypto.ts` | 加密工具 |

## OAuth 流程

```
1. 发起授权请求
   GET /oauth/authorize?client_id=...&redirect_uri=...

2. 用户在浏览器中登录并授权

3. 回调到 redirect_uri
   /callback?code=AUTH_CODE

4. 交换授权码
   POST /oauth/token
   { code: AUTH_CODE, client_secret: ... }

5. 获取访问令牌
   { access_token: "...", refresh_token: "..." }
```

## 令牌管理

### 自动刷新
```typescript
// 令牌过期前自动刷新
const token = await oauth.ensureValidToken()
// 如果快过期，自动使用 refresh_token 获取新令牌
```

### 安全存储
- 访问令牌加密存储
- 不存储在日志或错误信息中
- 内存中最小化暴露

## 支持的 OAuth 提供商

| 提供商 | 用途 |
|--------|------|
| Claude.ai | API 访问 |
| GitHub | 仓库操作 |
| Google | 云服务集成 |

## 端口管理

`oauthPort.ts` 管理本地 OAuth 回调监听端口，避免冲突。
