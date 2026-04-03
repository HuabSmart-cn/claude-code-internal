# services/autoDream - 自动 Dream 模式

## 功能

AutoDream 提供一个放松的探索模式，用户可以自由聊天而不会触发任何工具调用。

## 文件列表

| 文件 | 功能 |
|------|------|
| `autoDream.ts` | 核心逻辑 |
| `consolidationLock.ts` | 合并锁机制 |
| `consolidationPrompt.ts` | 合并提示词 |
| `config.ts` | 配置 |

## Dream 模式特性

### 1. 无工具模式
- 不执行任何工具
- 不修改任何文件
- 仅进行对话

### 2. 思维探索
- 可以讨论代码但不会实际修改
- 适合代码审查和设计讨论
- 安全的学习和探索环境

## 合并锁机制

`consolidationLock.ts` 防止在 Dream 模式下的更改被意外提交。

```typescript
// Dream 模式下自动加锁
if (isDreamMode()) {
  enableConsolidationLock()
}
```

## 配置

```typescript
interface AutoDreamConfig {
  enabled: boolean
  consolidationLock: boolean  // 是否启用合并锁
  maxSessionMinutes: number  // 最大会话时长
}
```
