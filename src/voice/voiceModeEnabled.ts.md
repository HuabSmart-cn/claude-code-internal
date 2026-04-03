# voiceModeEnabled.ts - 语音模式功能开关

## 文件概述
**路径**: `src/voice/voiceModeEnabled.ts`
**功能**: 提供语音模式的运行时检查，包括 GrowthBook 特性开关和 OAuth 认证状态

---

## 核心概念
- **GrowthBook 特性开关**: 通过 `tengu_amber_quartz_disabled` 标志控制语音模式 kill-switch
- **OAuth 认证**: 语音模式需要有效的 Anthropic OAuth token
- **多层检查**: `isVoiceModeEnabled()` 需要同时满足认证和特性开关两个条件
- **记忆化**: 使用 `getClaudeAIOAuthTokens()` 记忆化，首次调用约 20-50ms，后续为缓存命中

## 核心函数

```typescript
/**
 * GrowthBook kill-switch 检查
 * 除非 tengu_amber_quartz_disabled 标志为 true，否则返回 true
 */
export function isVoiceGrowthBookEnabled(): boolean

/**
 * 仅认证检查
 * 需要有效的 Anthropic OAuth token
 */
export function hasVoiceAuth(): boolean

/**
 * 完整运行时检查：认证 + GrowthBook kill-switch
 */
export function isVoiceModeEnabled(): boolean
```

## 检查逻辑

```
isVoiceModeEnabled()
    ├── hasVoiceAuth() // OAuth token 存在
    │   └── isAnthropicAuthEnabled() // 认证提供商检查
    │   └── getClaudeAIOAuthTokens()?.accessToken // token 有效性
    └── isVoiceGrowthBookEnabled() // GrowthBook 开关
        └── !getFeatureValue_CACHED_MAY_BE_STALE('tengu_amber_quartz_disabled', false)
```

## 注意事项
- 语音模式需要 Anthropic OAuth，不适用于 API key、Bedrock、Vertex 或 Foundry
- `isVoiceModeEnabled()` 用于命令时间和配置 UI
- React 渲染路径应使用 `useVoiceEnabled()`（有记忆化）

## 中英对照
| English | 中文 |
|---------|------|
| Voice Mode | 语音模式 |
| Voice GrowthBook Enabled | 语音 GrowthBook 启用 |
| Kill Switch | 强制关闭开关 |
| OAuth Auth | OAuth 认证 |
| Access Token | 访问令牌 |
| Feature Gate | 特性门控 |
| GrowthBook | GrowthBook 特性管理平台 |
| Enabled | 启用 |
| Disabled | 禁用 |
| Session-stable | 会话稳定 |
