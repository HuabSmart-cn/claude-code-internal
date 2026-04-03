# task/ - 任务管理

## 功能概述

`task/` 目录处理任务输出和格式化。

## 文件列表

```
task/
├── diskOutput.ts        # 磁盘输出
├── framework.ts        # 框架
├── outputFormatting.ts # 输出格式化
├── sdkProgress.ts     # SDK 进度
├── TaskOutput.ts      # 任务输出
└── types.ts           # 类型定义
```

## 任务输出

### TaskOutput
`TaskOutput.ts` - 核心任务输出类。

### 磁盘输出
`diskOutput.ts` - 将任务输出持久化到磁盘。

## 格式化

`outputFormatting.ts` - 格式化任务输出用于显示。
