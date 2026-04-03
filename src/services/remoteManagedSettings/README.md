# services/remoteManagedSettings - 远程托管设置

## 功能

remoteManagedSettings 服务允许管理员远程管理用户/团队的 Claude Code 设置。

## 文件列表

| 文件 | 功能 |
|------|------|
| `index.ts` | 远程设置管理 (17KB) |
| `types.ts` | 类型定义 |

## 设置类型

### 1. 用户级设置
- 默认权限策略
- 允许的工具列表
- UI 偏好

### 2. 团队级设置
- 共享的 MCP 服务器配置
- 团队记忆可见性
- 插件白名单

### 3. 组织级策略
- 数据保留策略
- 审计日志配置
- 安全策略

## 优先级

```
组织策略 > 团队设置 > 用户设置 > 本地设置
```

## 同步机制

```typescript
// 定期检查远程更新
await remoteSettings.checkForUpdates()

// 强制刷新
await remoteSettings.forceRefresh()
```

## 安全性

- 设置变更需要管理员权限
- 更改会被审计日志记录
- 敏感设置加密传输
