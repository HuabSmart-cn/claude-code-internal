# hooks/notifs - 通知系统

## 功能

通知系统负责向用户展示各种系统状态、警告和提示信息。

## 文件列表

### 核心文件
| 文件 | 功能 |
|------|------|
| `useStartupNotification.ts` | 启动时一次性通知 |
| `useRateLimitWarningNotification.tsx` | 速率限制警告 |
| `useMcpConnectivityStatus.tsx` | MCP 连接状态通知 |
| `useIDEStatusIndicator.tsx` | IDE 状态指示器 (20KB) |
| `usePluginAutoupdateNotification.tsx` | 插件自动更新通知 |
| `usePluginInstallationStatus.tsx` | 插件安装状态 (12KB) |
| `useLspInitializationNotification.tsx` | LSP 初始化通知 (16KB) |
| `useFastModeNotification.tsx` | 快速模式通知 (14KB) |
| `useModelMigrationNotifications.tsx` | 模型迁移通知 |
| `useDeprecationWarningNotification.tsx` | 弃用警告 |
| `useCanSwitchToExistingSubscription.tsx` | 订阅切换提示 |
| `useAutoModeUnavailableNotification.ts` | 自动模式不可用 |
| `useNpmDeprecationNotification.tsx` | NPM 弃用通知 |
| `useInstallMessages.tsx` | 安装消息 |
| `useSettingsErrors.tsx` | 设置错误通知 |
| `useTeammateShutdownNotification.ts` | 队友关闭通知 |

## 使用模式

```typescript
// 启动通知示例
const { addNotification } = useNotifications()
useStartupNotification(() => ({
  key: 'welcome',
  priority: 'normal',
  jsx: <Text>Welcome!</Text>
}))
```

## 通知优先级
- `immediate` - 立即显示
- `high` - 高优先级
- `normal` - 普通优先级
- `low` - 低优先级
