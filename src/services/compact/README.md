# services/compact - 上下文压缩

## 功能

上下文压缩服务通过智能减少对话历史来管理 Token 使用，确保长对话不会超出模型限制。

## 文件列表

| 文件 | 功能 | 大小 |
|------|------|------|
| `compact.ts` | 压缩核心逻辑 | 60KB |
| `microCompact.ts` | 微压缩（轻量级） | 19KB |
| `autoCompact.ts` | 自动压缩触发器 | 12KB |
| `sessionMemoryCompact.ts` | 会话内存压缩 | 21KB |
| `prompt.ts` | Prompt 压缩 | 16KB |
| `apiMicrocompact.ts` | API 微压缩 | 4KB |
| `grouping.ts` | 消息分组 | 2KB |
| `postCompactCleanup.ts` | 压缩后清理 | 3KB |
| `compactWarningHook.ts` | 压缩警告 Hook | 568B |
| `compactWarningState.ts` | 警告状态 | 693B |
| `timeBasedMCConfig.ts` | 基于时间的配置 | 1KB |

## 压缩策略

### 1. 微压缩 (microCompact)
轻量级压缩，保留关键信息:
- 系统提示
- 最近的对话轮次
- 工具定义

### 2. 完整压缩 (compact)
深度压缩流程:
1. 分析对话历史
2. 识别重要信息
3. 生成摘要
4. 替换原始消息

### 3. 会话内存压缩 (sessionMemoryCompact)
将对话内容提取为结构化记忆:
- 决策记录
- 偏好设置
- 上下文要点

## 触发时机

| 策略 | 触发条件 |
|------|----------|
| `autoCompact` | Token 达到阈值 (85%) |
| `timeBasedMCConfig` | 定时压缩 |
| `manual` | 用户触发 `/compact` |

## 压缩配置

```typescript
interface CompactConfig {
  maxTokens: number           // 最大保留 Token
  compressionRatio: number    // 压缩比 (0.0-1.0)
  preserveRecentTurns: number  // 保留最近轮次
  includeSummary: boolean      // 是否包含摘要
}
```

## 与 SessionMemory 的关系

```
compact.ts
    └── sessionMemoryCompact.ts
            └── SessionMemory/sessionMemory.ts
```

压缩后的内容会存入 SessionMemory 供后续参考。
