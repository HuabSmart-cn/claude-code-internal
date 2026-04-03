# SleepTool

## 功能

延迟执行一段时间。

## 核心文件

- `SleepTool.ts` - 主工具实现
- `prompt.ts` - 提示词

## 关键类型/函数

```typescript
interface SleepInput {
  duration_ms: number       // 延迟毫秒数
}
```

## 对应命令/用途

SleepTool 用于在特定场景下延迟操作。

**条件**：仅在 `PROACTIVE` 或 `KAIROS` 功能开启时可用。
