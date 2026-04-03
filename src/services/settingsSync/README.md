# services/settingsSync - 设置同步

## 功能

settingsSync 服务在多设备间同步用户设置和偏好。

## 文件列表

| 文件 | 功能 |
|------|------|
| `index.ts` | 同步核心 |
| `types.ts` | 类型定义 |

## 同步内容

### 用户设置
```typescript
interface SyncedSettings {
  theme: 'light' | 'dark' | 'system'
  fontSize: number
  keybindings: Record<string, string>
  // ...
}
```

### 工作区设置
```typescript
interface WorkspaceSettings {
  lspServers: Record<string, LSPConfig>
  mcpServers: Record<string, MCPConfig>
  customTools: ToolConfig[]
}
```

## 同步策略

### 1. 实时同步
设置变更后立即推送到云端。

### 2. 定期同步
定期检查并合并更改。

### 3. 冲突处理
- Last-write-wins (默认)
- 手动合并 (冲突时)

## 存储位置

```typescript
// 本地
~/.config/claude-code/settings.json

// 远程
Claude Cloud / 自定义服务器
```
