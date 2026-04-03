# model/ - 模型管理

## 功能概述

`model/` 目录负责 Claude 模型的选择、配置和能力管理。

## 文件列表

```
model/
├── agent.ts              # Agent 模型
├── aliases.ts           # 模型别名
├── antModels.ts         # ANT 模型
├── bedrock.ts           # Bedrock 配置
├── check1mAccess.ts     # 1M 访问检查
├── configs.ts           # 模型配置
├── contextWindowUpgradeCheck.ts  # 上下文窗口升级检查
├── deprecation.ts       # 废弃模型
├── model.ts             # 核心模型逻辑
├── modelAllowlist.ts    # 模型白名单
├── modelCapabilities.ts # 模型能力
├── modelOptions.ts      # 模型选项
├── modelStrings.ts      # 模型字符串
├── modelSupportOverrides.ts  # 支持覆盖
├── providers.ts         # 提供商
├── validateModel.ts    # 模型验证
└── apiQueryHookHelper.ts  # API 查询钩子
```

## 核心类型

### ModelOption
```typescript
interface ModelOption {
  name: string
  provider: string
  capabilities: ModelCapabilities
  contextWindow: number
  // ...
}
```

### ModelCapabilities
```typescript
interface ModelCapabilities {
  supportsPromptCache?: boolean
  supportsThought?: boolean
  maxOutputTokens?: number
  // ...
}
```

## 核心函数

### validateModel(modelName: string)
验证模型是否可用。

```typescript
export function validateModel(modelName: string): ValidationResult
```

### getModelCapabilities(modelName: string)
获取模型能力。

```typescript
export function getModelCapabilities(modelName: string): ModelCapabilities
```

### check1mAccess()
检查 Sonnet 1M 访问权限。

```typescript
export function check1mAccess(): Promise<{ hasAccess: boolean; ... }>
```

## 模型配置

### 模型白名单
`modelAllowlist.ts` - 定义允许使用的模型列表。

### 模型别名
`aliases.ts` - 模型名称别名映射。

## 主要模型

- Claude 3.5 Sonnet
- Claude 3 Opus
- Claude 3 Haiku
- Sonnet 4
- Sonnet 4.5 1M
