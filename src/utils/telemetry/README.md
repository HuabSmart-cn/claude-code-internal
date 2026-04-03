# telemetry/ - 遥测数据

## 功能概述

`telemetry/` 目录收集和导出使用分析和性能数据。

## 文件列表

```
telemetry/
├── betaSessionTracing.ts  # Beta 会话追踪
├── bigqueryExporter.ts    # BigQuery 导出
├── events.ts             # 事件定义
├── instrumentation.ts    # 插桩
├── logger.ts            # 日志
├── perfettoTracing.ts   # Perfetto 追踪
├── pluginTelemetry.ts   # 插件遥测
├── sessionTracing.ts    # 会话追踪
└── skillLoadedEvent.ts  # 技能加载事件
```

## 追踪系统

### Perfetto
`perfettoTracing.ts` - 使用 Perfetto 进行性能追踪。

### 会话追踪
`sessionTracing.ts` - 追踪用户会话事件。

### Beta 追踪
`betaSessionTracing.ts` - Beta 功能的特殊追踪。

## 数据导出

### BigQuery
`bigqueryExporter.ts` - 将遥测数据导出到 BigQuery。

## 事件

`events.ts` 定义所有遥测事件类型。

## 插桩

`instrumentation.ts` - 自动化代码插桩。
