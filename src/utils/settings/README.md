# settings/ - 设置管理

## 功能概述

`settings/` 目录管理 Claude Code 的各种设置。

## 文件列表

```
settings/
├── allErrors.ts           # 所有错误定义
├── applySettingsChange.ts # 应用设置更改
├── changeDetector.ts     # 更改检测
├── constants.ts           # 常量
├── internalWrites.ts     # 内部写入
├── managedPath.ts         # 托管路径
├── mdm/                  # MDM 配置
├── permissionValidation.ts # 权限验证
├── pluginOnlyPolicy.ts    # 插件策略
├── schemaOutput.ts        # Schema 输出
├── settings.ts           # 设置主文件
├── settingsCache.ts       # 设置缓存
├── toolValidationConfig.ts # 工具验证配置
├── types.ts              # 类型定义
├── validateEditTool.ts    # 验证编辑工具
├── validation.ts         # 验证
└── validationTips.ts     # 验证提示
```

## 设置来源

### 用户设置
`~/.claude/settings.json`

### 项目设置
`./.claude/settings.json`

### 托管设置 (MDM)
`mdm/` 目录 - 企业移动设备管理

## 设置类型

### 工具设置
哪些工具可用。

### 权限规则
工具使用的权限规则。

### 钩子配置
各种钩子的配置。

## 验证

`validation.ts` - 验证设置文件的结构和值。
