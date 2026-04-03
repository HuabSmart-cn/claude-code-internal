# services/analytics - 分析服务

## 功能

分析服务负责收集、聚合和导出使用数据和实验配置。

## 文件列表

| 文件 | 功能 | 大小 |
|------|------|------|
| `growthbook.ts` | GrowthBook A/B 测试框架 | 40KB |
| `metadata.ts` | 分析元数据收集 | 32KB |
| `firstPartyEventLogger.ts` | 第一方事件日志 | 14KB |
| `firstPartyEventLoggingExporter.ts` | 事件导出器 | 26KB |
| `datadog.ts` | DataDog 集成 | 9KB |
| `sink.ts` | 日志接收器 | 3KB |
| `sinkKillswitch.ts` | 接收器开关 | 1KB |
| `index.ts` | 入口文件 | 5KB |
| `config.ts` | 配置文件 | 1KB |

## 核心组件

### growthbook.ts
GrowthBook SDK 集成:
- Feature Flag 评估
- A/B 测试配置
- 实验分组

### metadata.ts
收集的元数据类型:
- 工具使用统计
- Token 使用量
- 会话持续时间
- 错误频率

## 事件类型

```typescript
type AnalyticsEvent =
  | { type: 'tool_use'; tool: string; duration: number }
  | { type: 'api_call'; model: string; tokens: number }
  | { type: 'compact'; tokensSaved: number }
  | { type: 'error'; errorType: string }
```

## 数据流向

```
用户操作 → metadata.ts → firstPartyEventLogger.ts
                                    ↓
                            growthbook.ts (实验)
                                    ↓
                            DataDog / 自定义接收器
```

## 隐私保护

- 敏感路径自动过滤
- 用户可选择退出分析
- 本地处理后脱敏再发送
