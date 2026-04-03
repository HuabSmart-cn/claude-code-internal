# services/tips - 提示系统

## 功能

Tips 服务向用户展示使用技巧和新功能介绍。

## 文件列表

| 文件 | 功能 | 大小 |
|------|------|------|
| `tipRegistry.ts` | 提示注册表 | 23KB |
| `tipScheduler.ts` | 提示调度器 | 1KB |
| `tipHistory.ts` | 提示历史 | 601B |

## 提示类型

### 1. 欢迎提示
首次使用时的功能介绍。

### 2. 上下文提示
根据用户行为展示相关技巧。

### 3. 新功能提示
版本更新时的功能介绍。

## 调度策略

```typescript
interface TipSchedule {
  trigger: 'on-event' | 'on-timer' | 'on-context'
  event?: string
  interval?: number  // 毫秒
  contextMatch?: (ctx: Context) => boolean
}
```

## 提示显示规则

- 不打扰用户工作
- 可手动关闭
- 不重复显示相同提示
- 根据用户经验级别调整
