# services/plugins - 插件系统

## 功能

插件系统允许扩展 Claude Code 功能，支持第三方集成和自定义工具。

## 文件列表

| 文件 | 功能 | 大小 |
|------|------|------|
| `index.ts` | 插件核心 | 44KB |
| `pluginOperations.ts` | 插件操作 | 35KB |
| `PluginInstallationManager.ts` | 安装管理 | 6KB |
| `pluginCliCommands.ts` | CLI 命令 | 10KB |
| `secretScanner.ts` | 密钥扫描 | 9KB |
| `watcher.ts` | 文件监视 | 13KB |
| `teamMemSecretGuard.ts` | 团队记忆保护 | 1KB |
| `types.ts` | 类型定义 | 4KB |

## 插件操作

### 安装
```typescript
await pluginManager.install('plugin-name')
```

### 卸载
```typescript
await pluginManager.uninstall('plugin-name')
```

### 更新
```typescript
await pluginManager.update('plugin-name', '1.0.1')
```

## 插件结构

```
plugins/
└── my-plugin/
    ├── plugin.json       # 插件元数据
    ├── dist/             # 编译后的代码
    └── package.json
```

### plugin.json
```json
{
  "name": "my-plugin",
  "version": "1.0.0",
  "description": "My Claude Code plugin",
  "tools": [{ "name": "myTool", "path": "./dist/tool.js" }],
  "hooks": { "preToolExecution": "./dist/hook.js" }
}
```

## 安全机制

### secretScanner.ts
扫描插件中可能的:
- API Keys
- 密码
- 私钥
- 其他敏感信息

### teamMemSecretGuard.ts
保护团队记忆中的敏感数据不被插件访问。

## 生命周期

1. **Discover** - 发现可用插件
2. **Install** - 下载和安装
3. **Enable** - 激活插件
4. **Run** - 执行插件代码
5. **Disable** - 停用插件
6. **Uninstall** - 卸载插件
