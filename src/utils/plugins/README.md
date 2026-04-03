# plugins/ - 插件系统

## 功能概述

`plugins/` 目录是 Claude Code 的插件管理系统，是最大的子目录之一。

## 文件列表 (46 个文件)

```
plugins/
├── addDirPluginSettings.ts      # 添加目录插件设置
├── cacheUtils.ts               # 缓存工具
├── dependencyResolver.ts       # 依赖解析
├── fetchTelemetry.ts          # 获取遥测
├── gitAvailability.ts         # Git 可用性
├── headlessPluginInstall.ts   # 无头插件安装
├── hintRecommendation.ts     # 提示推荐
├── installCounts.ts           # 安装计数
├── installedPluginsManager.ts # 已安装插件管理
├── loadPluginAgents.ts        # 加载插件 Agent
├── loadPluginCommands.ts      # 加载插件命令
├── loadPluginHooks.ts         # 加载插件钩子
├── loadPluginOutputStyles.ts  # 加载插件输出样式
├── lspPluginIntegration.ts   # LSP 插件集成
├── lspRecommendation.ts       # LSP 推荐
├── managedPlugins.ts          # 托管插件
├── marketplaceHelpers.ts      # 市场助手
├── marketplaceManager.ts     # 市场管理 (93KB)
├── mcpbHandler.ts            # MCPB 处理器
├── mcpPluginIntegration.ts   # MCP 插件集成
├── officialMarketplace.ts    # 官方市场
├── officialMarketplaceGcs.ts # 官方市场 GCS
├── officialMarketplaceStartupCheck.ts  # 启动检查
├── orphanedPluginFilter.ts    # 孤立插件过滤
├── parseMarketplaceInput.ts   # 解析市场输入
├── performStartupChecks.tsx  # 执行启动检查
├── pluginAutoupdate.ts       # 插件自动更新
├── pluginBlocklist.ts       # 插件黑名单
├── pluginDirectories.ts     # 插件目录
├── pluginFlagging.ts        # 插件标记
├── pluginIdentifier.ts      # 插件标识符
├── pluginInstallationHelpers.ts  # 安装助手
├── pluginLoader.ts          # 插件加载器 (110KB)
├── pluginOptionsStorage.ts  # 选项存储
├── pluginPolicy.ts         # 插件策略
├── pluginStartupCheck.ts   # 启动检查
├── pluginVersioning.ts     # 版本管理
├── reconciler.ts           # 调停者
├── refresh.ts             # 刷新
├── schemas.ts             # Schema 定义 (59KB)
├── validatePlugin.ts      # 验证插件
├── walkPluginMarkdown.ts  # 遍历 Markdown
├── zipCache.ts           # ZIP 缓存
└── zipCacheAdapters.ts   # ZIP 缓存适配器
```

## 插件生命周期

### 安装
`headlessPluginInstall.ts` - 无头安装
`marketplaceManager.ts` - 市场管理

### 加载
`pluginLoader.ts` - 核心加载器
`loadPluginAgents.ts` - 加载 Agent
`loadPluginCommands.ts` - 加载命令
`loadPluginHooks.ts` - 加载钩子

### 验证
`validatePlugin.ts` - 插件验证
`schemas.ts` - Schema 验证

## 插件市场

### 官方市场
`officialMarketplace.ts` - 官方插件市场
`officialMarketplaceGcs.ts` - GCS 集成

### 市场管理
`marketplaceManager.ts` - 市场 CRUD 操作

## 插件类型

### MCP 插件
`mcpPluginIntegration.ts` - MCP 协议集成

### LSP 插件
`lspPluginIntegration.ts` - Language Server Protocol

### Agent 插件
自定义 AI Agent。

## 依赖管理

`dependencyResolver.ts` - 解析插件依赖关系。

## 版本管理

`pluginVersioning.ts` - 插件版本控制。

## 自动更新

`pluginAutoupdate.ts` - 插件自动更新机制。
