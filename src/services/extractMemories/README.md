# services/extractMemories - 记忆提取

## 功能

从对话历史中提取结构化信息，用于增强 AI 的上下文理解。

## 文件列表

| 文件 | 功能 |
|------|------|
| `extractMemories.ts` | 记忆提取核心 (21KB) |
| `prompts.ts` | 提取提示词 |

## 提取的信息类型

### 1. 项目知识
```typescript
interface ProjectKnowledge {
  language: string[]           // 编程语言
  frameworks: string[]         // 框架
  architecture: string        // 架构模式
  keyFiles: string[]          // 关键文件
}
```

### 2. 用户偏好
```typescript
interface UserPreferences {
  codeStyle: string           // 代码风格
  tools: string[]             // 常用工具
  workflow: string             // 工作流程
}
```

### 3. 决策记录
```typescript
interface Decisions {
  decision: string            // 决策内容
  reason: string              // 决策原因
  timestamp: number           // 时间戳
}
```

## 提取流程

```
对话消息
    ↓
prompts.ts 格式化
    ↓
AI 分析
    ↓
结构化输出
    ↓
存储到 SessionMemory
```

## 与 SessionMemory 的区别

| 特性 | extractMemories | SessionMemory |
|------|-----------------|---------------|
| 触发时机 | 每条消息后 | 定期/阈值触发 |
| 粒度 | 细粒度提取 | 粗粒度总结 |
| 内容 | 具体事实 | 抽象概括 |
| 用途 | RAG 检索 | 上下文补充 |
