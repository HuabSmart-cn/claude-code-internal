# services/SessionMemory - 会话内存

## 功能

SessionMemory 服务自动维护当前对话的结构化记忆，以 Markdown 格式记录关键信息。

## 文件列表

| 文件 | 功能 |
|------|------|
| `sessionMemory.ts` | 会话内存核心 |
| `sessionMemoryUtils.ts` | 工具函数 |
| `prompts.ts` | 提示词模板 |

## 工作原理

```
┌─────────────────┐
│  对话消息流     │
└────────┬────────┘
         ↓
┌─────────────────┐
│ 定期提取检查    │ ← 触发阈值: Token 数量或消息数
└────────┬────────┘
         ↓
┌─────────────────┐
│ Forked Subagent │ ← 后台运行，不阻塞主对话
└────────┬────────┘
         ↓
┌─────────────────┐
│ 生成结构化摘要   │
└────────┬────────┘
         ↓
┌─────────────────┐
│ 写入 .session/   │ ← 持久化到磁盘
└─────────────────┘
```

## 记忆内容

### 提取的信息类型
- **决策记录**: 用户做出的重要选择
- **偏好设置**: 用户的工作习惯和偏好
- **上下文要点**: 项目的关键信息
- **待办事项**: 需要完成的任务
- **问题解决**: 已解决的问题方案

## 配置

```typescript
interface SessionMemoryConfig {
  enabled: boolean
  updateInterval: number      // 更新间隔 (消息数)
  minTokensForUpdate: number  // 最小 Token 数
  maxMemoryTokens: number     // 最大记忆 Token
  extractionPrompt: string    // 提取提示词
}
```

## 文件位置

```
.project/.session/
└── memory.md  // 会话记忆文件
```

## 与 Compact 的关系

SessionMemory 是 Compact 的补充:
- **Compact**: 减少对话历史，保留近期的上下文
- **SessionMemory**: 提取关键信息，长期保留

两者结合确保:
1. Token 使用可控
2. 重要信息不丢失
