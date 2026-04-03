# Hooks 目录

## 概述

Hooks 目录包含 83 个 React Hook 文件，提供状态管理、权限控制、通知、IDE 集成等功能。

## 目录结构

```
hooks/
├── notifs/                    # 通知相关 hooks
│   ├── handlers/
│   ├── PermissionContext.ts
│   └── permissionLogging.ts
├── toolPermission/            # 工具权限相关
│   └── handlers/             # 权限处理程序
├── *.ts / *.tsx              # 各功能 hooks
```

## 分类

### 1. 工具权限 (Tool Permission)
| 文件 | 功能 |
|------|------|
| `useCanUseTool.tsx` | 核心权限检查 hook，管理工具使用权限流程 |
| `toolPermission/PermissionContext.ts` | 权限上下文管理 |
| `toolPermission/permissionLogging.ts` | 权限决策日志记录 |

### 2. 通知 (Notifications)
| 文件 | 功能 |
|------|------|
| `notifs/useStartupNotification.ts` | 启动通知 |
| `notifs/useRateLimitWarningNotification.tsx` | 速率限制警告 |
| `notifs/useMcpConnectivityStatus.tsx` | MCP 连接状态 |
| `notifs/useIDEStatusIndicator.tsx` | IDE 状态指示器 |
| `notifs/usePluginAutoupdateNotification.tsx` | 插件自动更新通知 |
| `notifs/usePluginInstallationStatus.tsx` | 插件安装状态 |
| `notifs/useLspInitializationNotification.tsx` | LSP 初始化通知 |

### 3. 状态管理
| 文件 | 功能 |
|------|------|
| `useSettings.ts` | 设置管理 |
| `useAppState.ts` | 应用状态 |
| `useMergedClients.ts` | 合并客户端状态 |
| `useMergedCommands.ts` | 合并命令 |
| `useMergedTools.ts` | 合并工具 |

### 4. IDE 集成
| 文件 | 功能 |
|------|------|
| `useIDEIntegration.tsx` | IDE 集成核心 |
| `useDiffInIDE.ts` | IDE 差异对比 |
| `useIdeSelection.ts` | IDE 选择状态 |
| `useIdeAtMentioned.ts` | @提及处理 |
| `useIdeConnectionStatus.ts` | IDE 连接状态 |

### 5. 语音/输入
| 文件 | 功能 |
|------|------|
| `useVoice.ts` | 语音输入核心 (45KB) |
| `useVoiceIntegration.tsx` | 语音集成 (99KB) |
| `useTextInput.ts` | 文本输入处理 |
| `usePasteHandler.ts` | 粘贴处理 |
| `useSearchInput.ts` | 搜索输入 |

### 6. 历史/撤销
| 文件 | 功能 |
|------|------|
| `useArrowKeyHistory.tsx` | 方向键历史导航 |
| `useAssistantHistory.ts` | 助手历史管理 |
| `useHistorySearch.ts` | 历史搜索 |
| `useTurnDiffs.ts` | 轮次差异对比 |

### 7. 任务管理
| 文件 | 功能 |
|------|------|
| `useTasksV2.ts` | 任务管理 v2 |
| `useTaskListWatcher.ts` | 任务列表监视 |
| `useQueueProcessor.ts` | 队列处理 |

### 8. 远程会话
| 文件 | 功能 |
|------|------|
| `useRemoteSession.ts` | 远程会话管理 (23KB) |
| `useSSHSession.ts` | SSH 会话管理 |

### 9. 插件管理
| 文件 | 功能 |
|------|------|
| `useManagePlugins.ts` | 插件管理 (11KB) |
| `usePluginRecommendationBase.tsx` | 插件推荐基础 |

### 10. LSP 相关
| 文件 | 功能 |
|------|------|
| `useLspPluginRecommendation.tsx` | LSP 插件推荐 (21KB) |

### 11. 其他
| 文件 | 功能 |
|------|------|
| `useCanUseTool.tsx` | 权限检查核心 (40KB) |
| `useTypeahead.tsx` | 自动补全 (212KB，最大文件) |
| `useGlobalKeybindings.tsx` | 全局快捷键 (31KB) |
| `useInboxPoller.ts` | 收件箱轮询 (34KB) |
| `useReplBridge.tsx` | REPL 桥接 (115KB) |
| `useCancelRequest.ts` | 请求取消 (10KB) |
| `useCommandKeybindings.tsx` | 命令快捷键 (11KB) |
| `useClipboardImageHint.ts` | 剪贴板图片提示 |

## 权限处理子目录

### toolPermission/handlers/
| 文件 | 功能 |
|------|------|
| `coordinatorHandler.ts` | 协调器权限处理 |
| `interactiveHandler.ts` | 交互式权限处理 (20KB) |
| `swarmWorkerHandler.ts` | Swarm Worker 权限处理 |
