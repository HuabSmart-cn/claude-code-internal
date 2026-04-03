# Services 目录

## 概述

Services 目录包含 38 个子目录，提供 API 调用、上下文压缩、工具执行、MCP 协议实现、会话内存等核心服务。

## 目录结构

```
services/
├── AgentSummary/              # Agent 摘要
├── analytics/                  # 分析服务
├── api/                       # API 调用
├── autoDream/                 # 自动 Dream
├── compact/                   # 上下文压缩
├── extractMemories/           # 记忆提取
├── lsp/                       # 语言服务器协议
├── MagicDocs/                 # 文档生成
├── mcp/                       # MCP 协议
├── oauth/                     # OAuth 认证
├── plugins/                   # 插件管理
├── policyLimits/              # 策略限制
├── PromptSuggestion/          # 提示建议
├── remoteManagedSettings/     # 远程托管设置
├── SessionMemory/             # 会话内存
├── settingsSync/              # 设置同步
├── teamMemorySync/            # 团队记忆同步
├── tips/                      # 提示系统
├── tools/                     # 工具执行
├── toolUseSummary/            # 工具使用摘要
```

## 分类

### 1. API 层 (api/)
| 文件 | 功能 |
|------|------|
| `claude.ts` | Claude API 调用核心 (125KB) |
| `client.ts` | API 客户端 (161KB) |
| `errors.ts` | API 错误处理 (41KB) |
| `withRetry.ts` | 重试逻辑 (28KB) |
| `grove.ts` | Grove API 集成 |
| `logging.ts` | API 日志 |
| `filesApi.ts` | 文件 API |
| `sessionIngress.ts` | 会话入口管理 |

### 2. 上下文压缩 (compact/)
| 文件 | 功能 |
|------|------|
| `compact.ts` | 压缩核心 (60KB) |
| `microCompact.ts` | 微压缩 (19KB) |
| `autoCompact.ts` | 自动压缩 (12KB) |
| `sessionMemoryCompact.ts` | 会话内存压缩 |
| `prompt.ts` | 提示词压缩 |
| `apiMicrocompact.ts` | API 微压缩 |
| `grouping.ts` | 消息分组 |

### 3. 工具执行 (tools/)
| 文件 | 功能 |
|------|------|
| `toolExecution.ts` | 工具执行核心 (60KB) |
| `StreamingToolExecutor.ts` | 流式工具执行器 |
| `toolHooks.ts` | 工具钩子 (22KB) |
| `toolOrchestration.ts` | 工具编排 |

### 4. MCP 协议 (mcp/)
| 文件 | 功能 |
|------|------|
| `client.ts` | MCP 客户端 (118KB) |
| `auth.ts` | MCP 认证 (88KB) |
| `config.ts` | MCP 配置 (51KB) |
| `useManageMCPConnections.ts` | MCP 连接管理 (44KB) |
| `xaa.ts` | XAA 集成 |
| `channelPermissions.ts` | 渠道权限 |
| `elicitationHandler.ts` | 征询处理 |

### 5. 会话内存 (SessionMemory/)
| 文件 | 功能 |
|------|------|
| `sessionMemory.ts` | 会话内存核心 (16KB) |
| `sessionMemoryUtils.ts` | 会话内存工具 |
| `prompts.ts` | 提示词模板 |

### 6. 分析服务 (analytics/)
| 文件 | 功能 |
|------|------|
| `growthbook.ts` | GrowthBook A/B 测试 (40KB) |
| `metadata.ts` | 分析元数据 (32KB) |
| `firstPartyEventLogger.ts` | 第一方事件日志 |
| `firstPartyEventLoggingExporter.ts` | 事件导出 |
| `datadog.ts` | DataDog 集成 |
| `index.ts` | 入口文件 |

### 7. LSP 服务 (lsp/)
| 文件 | 功能 |
|------|------|
| `LSPClient.ts` | LSP 客户端 |
| `LSPServerInstance.ts` | LSP 服务器实例 |
| `LSPServerManager.ts` | LSP 服务器管理 |
| `LSPDiagnosticRegistry.ts` | 诊断注册 |
| `manager.ts` | 管理器 |
| `passiveFeedback.ts` | 被动反馈 |
| `prompts.ts` | LSP 提示词 |

### 8. 插件系统 (plugins/)
| 文件 | 功能 |
|------|------|
| `index.ts` | 插件核心 (44KB) |
| `pluginOperations.ts` | 插件操作 (35KB) |
| `PluginInstallationManager.ts` | 安装管理 |
| `pluginCliCommands.ts` | CLI 命令 |
| `secretScanner.ts` | 密钥扫描 |
| `watcher.ts` | 插件监视 |

### 9. 团队记忆同步 (teamMemorySync/)
| 文件 | 功能 |
|------|------|
| `index.ts` | 核心同步 (20KB) |
| `securityCheck.tsx` | 安全检查 (10KB) |
| `syncCache.ts` | 同步缓存 |
| `syncCacheState.ts` | 缓存状态 |
| `types.ts` | 类型定义 |

### 10. 设置同步 (settingsSync/)
| 文件 | 功能 |
|------|------|
| `index.ts` | 同步核心 (17KB) |
| `types.ts` | 类型定义 |

### 11. OAuth 认证 (oauth/)
| 文件 | 功能 |
|------|------|
| `client.ts` | OAuth 客户端 (18KB) |
| `auth-code-listener.ts` | 授权码监听 |
| `index.ts` | 入口文件 |
| `getOauthProfile.ts` | 获取 OAuth 个人资料 |

### 12. 提示建议 (PromptSuggestion/)
| 文件 | 功能 |
|------|------|
| `promptSuggestion.ts` | 提示建议 (17KB) |
| `speculation.ts` | 推测补全 (30KB) |

### 13. 记忆提取 (extractMemories/)
| 文件 | 功能 |
|------|------|
| `extractMemories.ts` | 记忆提取 (21KB) |
| `prompts.ts` | 提取提示词 |

### 14. 自动 Dream (autoDream/)
| 文件 | 功能 |
|------|------|
| `autoDream.ts` | 自动 Dream (11KB) |
| `consolidationLock.ts` | 合并锁 |
| `consolidationPrompt.ts` | 合并提示词 |
| `config.ts` | 配置 |

### 15. MagicDocs (MagicDocs/)
| 文件 | 功能 |
|------|------|
| `magicDocs.ts` | 文档生成 |
| `prompts.ts` | 提示词 |

### 16. 策略限制 (policyLimits/)
此目录提供速率限制和策略管理功能。

### 17. 提示系统 (tips/)
| 文件 | 功能 |
|------|------|
| `tipRegistry.ts` | 提示注册 (23KB) |
| `tipScheduler.ts` | 提示调度 |
| `tipHistory.ts` | 提示历史 |

### 18. 工具使用摘要 (toolUseSummary/)
| 文件 | 功能 |
|------|------|
| `toolUseSummaryGenerator.ts` | 摘要生成器 |

### 19. Agent 摘要 (AgentSummary/)
| 文件 | 功能 |
|------|------|
| `agentSummary.ts` | Agent 状态摘要 |

### 20. 远程托管设置 (remoteManagedSettings/)
| 文件 | 功能 |
|------|------|
| `index.ts` | 远程设置管理 |
| `types.ts` | 类型定义 |

## 服务间依赖

```
api/claude.ts          <-- 核心 API 调用
    └── tools/toolExecution.ts  <-- 工具执行
            └── compact/compact.ts  <-- 上下文压缩
                    └── SessionMemory/sessionMemory.ts  <-- 会话内存
```

## 关键流程

### 工具执行流程
1. `useCanUseTool.tsx` 检查权限
2. `tools/toolExecution.ts` 执行工具
3. `analytics/` 记录分析数据
4. `compact/` 管理上下文压缩

### MCP 协议流程
1. `mcp/client.ts` 管理连接
2. `mcp/auth.ts` 处理认证
3. `mcp/useManageMCPConnections.ts` 连接生命周期
