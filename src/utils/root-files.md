# utils/ 根目录文件分类

## 概述

utils/ 根目录包含约 270 个 TypeScript 文件，按功能分类如下：

## 文件操作类

| 文件 | 功能 |
|------|------|
| `file.ts` | 文件操作封装 |
| `fileRead.ts` | 文件读取 |
| `fileHistory.ts` | 文件历史记录 |
| `attachments.ts` | 附件处理 |
| `imagePaste.ts` | 图片粘贴 |
| `imageValidation.ts` | 图片验证 |
| `pdfUtils.ts` | PDF 工具 |
| `notebook.ts` | Jupyter notebook 支持 |
| `bufferedWriter.ts` | 缓冲写入 |
| `filePersistence.ts` | 文件持久化 |

## Git 操作类

| 文件 | 功能 |
|------|------|
| `git.ts` | Git 操作封装 |
| `gitDiff.ts` | Git 差异计算 |
| `gitFilesystem.ts` | Git 文件系统操作 |
| `detectRepository.ts` | 仓库检测 |
| `git/index.ts` | Git 子目录入口 |

## 消息处理类

| 文件 | 功能 |
|------|------|
| `messages.ts` | 消息创建和处理 |
| `messages/index.ts` | 消息子目录入口 |
| `tokens.ts` | Token 计算 |

## 权限与安全类

| 文件 | 功能 |
|------|------|
| `permissions.ts` | 权限管理入口 |
| `permissions/index.ts` | 权限子目录入口 |
| `sanitization.ts` |  sanitization |
| `secureStorage/index.ts` | 安全存储 |

## Shell 与命令类

| 文件 | 功能 |
|------|------|
| `bash.ts` | Bash 命令 |
| `shell.ts` | Shell 工具 |
| `shell/index.ts` | Shell 子目录入口 |
| `powershell/index.ts` | PowerShell 支持 |
| `shellQuote.ts` | Shell 引号 |
| `shellQuoting.ts` | Shell 引用规则 |

## 配置类

| 文件 | 功能 |
|------|------|
| `config.ts` | 全局配置 |
| `settings/index.ts` | 设置子目录入口 |
| `env.ts` | 环境变量 |
| `envUtils.ts` | 环境工具 |
| `path.ts` | 路径处理 |

## API 与网络类

| 文件 | 功能 |
|------|------|
| `api.ts` | API 调用 |
| `apiPreconnect.ts` | API 预连接 |
| `auth.ts` | 认证 |
| `claudeDesktop.ts` | Claude Desktop |
| `caCerts.ts` | CA 证书 |
| `caCertsConfig.ts` | CA 证书配置 |

## 模型类

| 文件 | 功能 |
|------|------|
| `model.ts` | 模型入口 |
| `model/index.ts` | 模型子目录入口 |
| `modelCost.ts` | 模型成本 |
| `modelGrounding.ts` | 模型接地 |

## MCP 类

| 文件 | 功能 |
|------|------|
| `mcp.ts` | MCP 入口 |
| `mcp/index.ts` | MCP 子目录 |
| `mcpUtils.ts` | MCP 工具 |

## 工具函数类

| 文件 | 功能 |
|------|------|
| `json.ts` | JSON 处理 |
| `jsonRead.ts` | JSON 读取 |
| `slowOperations.ts` | 慢操作优化 |
| `log.ts` | 日志 |
| `logError.ts` | 错误日志 |
| `error.ts` | 错误处理 |
| `errors.ts` | 错误类型 |
| `debug.ts` | 调试 |
| `diagLogs.ts` | 诊断日志 |
| `array.ts` | 数组工具 |
| `set.ts` | 集合工具 |
| `stringUtils.ts` | 字符串工具 |
| `escape.ts` | 转义 |
| `uuid.ts` | UUID 生成 |
| `semanticNumber.ts` | 语义数字 |
| `semanticBoolean.ts` | 语义布尔 |

## UI 组件类

| 文件 | 功能 |
|------|------|
| `display.ts` | 显示 |
| `displayTags.ts` | 显示标签 |
| `ansi.ts` | ANSI 转义 |
| `ansiToPng.ts` | ANSI 到 PNG |
| `ansiToSvg.ts` | ANSI 到 SVG |
| `asciicast.ts` | Asciicast |
| `imageResizer.ts` | 图片调整 |
| `imageDiff.ts` | 图片差异 |

## 状态管理类

| 文件 | 功能 |
|------|------|
| `state.ts` | 状态 |
| `agentContext.ts` | Agent 上下文 |
| `sessionActivity.ts` | 会话活动 |
| `cleanup.ts` | 清理 |
| `cleanupRegistry.ts` | 清理注册表 |

## 分析与遥测类

| 文件 | 功能 |
|------|------|
| `analytics.ts` | 分析 |
| `analytics/index.ts` | 分析子目录 |
| `telemetry/index.ts` | 遥测子目录入口 |
| `perf.ts` | 性能 |

## 特性开关类

| 文件 | 功能 |
|------|------|
| `feature.ts` | 特性开关 |
| `betas.ts` | Beta 功能 |
| `experiments.ts` | 实验功能 |

## 自动更新类

| 文件 | 功能 |
|------|------|
| `autoUpdater.ts` | 自动更新 |

## 启动类

| 文件 | 功能 |
|------|------|
| `bootstrap.ts` | 启动 |
| `startup.ts` | 启动流程 |

## 其他工具类

| 文件 | 功能 |
|------|------|
| `abortController.ts` | AbortController |
| `CircularBuffer.ts` | 循环缓冲 |
| `which.ts` | 命令查找 |
| `xdg.ts` | XDG 路径 |
| `cwd.ts` | 当前目录 |
| `clipboard.ts` | 剪贴板 |
| `hash.ts` | 哈希 |
| `platform.ts` | 平台检测 |
| `process.ts` | 进程 |
| `sleep.ts` | 睡眠 |
| `retry.ts` | 重试 |
| `once.ts` | 单次执行 |
| `memoize.ts` | 记忆化 |

## Claude.ai 集成类

| 文件 | 功能 |
|------|------|
| `claudeAi.ts` | Claude.ai |
| `claudeInChrome/index.ts` | Chrome 扩展 |

## 后台任务类

| 文件 | 功能 |
|------|------|
| `background.ts` | 后台任务 |
| `background/index.ts` | 后台子目录 |
| `backgroundHousekeeping.ts` | 后台维护 |

## 工作区类

| 文件 | 功能 |
|------|------|
| `workspace.ts` | 工作区 |
| `workspaceManifest.ts` | 工作区清单 |

## 建议类

| 文件 | 功能 |
|------|------|
| `suggestions/index.ts` | 建议子目录 |
| `claudeCodeHints.ts` | 代码提示 |

## Hooks 类

| 文件 | 功能 |
|------|------|
| `hooks.ts` | Hooks 入口 |
| `hooks/index.ts` | Hooks 子目录 |

## Swarm 类

| 文件 | 功能 |
|------|------|
| `swarm.ts` | Swarm 入口 |
| `swarm/index.ts` | Swarm 子目录 |

## 其他特定功能类

| 文件 | 功能 |
|------|------|
| `computerUse.ts` | 计算机使用 |
| `teleport.ts` | 远程 |
| `planMode.ts` | 计划模式 |
| `planModeV2.ts` | 计划模式 V2 |
| `task.ts` | 任务 |
| `task/index.ts` | 任务子目录 |
| `todo.ts` | Todo |
| `memory.ts` | 记忆 |
| `memory/index.ts` | 记忆子目录 |
| `skills.ts` | 技能 |
| `skills/index.ts` | 技能子目录 |
| `plugins.ts` | 插件入口 |
| `plugins/index.ts` | 插件子目录 |
| `marketplace.ts` | 市场 |
| `dxt.ts` | DXT 扩展 |
| `deepLink.ts` | Deep Link |
| `deepLink/index.ts` | Deep Link 子目录 |
| `autoRunIssue.tsx` | 自动运行问题 |
| `advisor.ts` | 顾问 |
| `swarmsEnabled.ts` | Swarm 启用 |

## 集成类

| 文件 | 功能 |
|------|------|
| `slack.ts` | Slack |
| `jira.ts` | Jira |
| `linear.ts` | Linear |
| `github.ts` | GitHub |
| `github/index.ts` | GitHub 子目录 |

## 完整分类汇总

```
根目录文件分类：

1. 文件操作 (file*, attachments, image*, pdf, notebook)
   - 约 25 个文件

2. Git 操作 (git*, detectRepository)
   - 约 8 个文件

3. 消息处理 (messages, tokens)
   - 约 5 个文件

4. 权限安全 (permissions, sanitization, secureStorage)
   - 约 10 个文件

5. Shell 命令 (bash, shell*, powershell)
   - 约 15 个文件

6. 配置 (config, settings, env*, path)
   - 约 20 个文件

7. API 网络 (api*, auth, claudeDesktop, caCerts)
   - 约 20 个文件

8. 模型 (model*, modelCost)
   - 约 10 个文件

9. MCP (mcp, mcpUtils)
   - 约 5 个文件

10. 工具函数 (json, log, error*, array, string, uuid, etc.)
    - 约 50 个文件

11. UI 显示 (display*, ansi*, asciicast, image*)
    - 约 20 个文件

12. 状态管理 (state, agentContext, cleanup*)
    - 约 15 个文件

13. 分析遥测 (analytics, telemetry*, perf)
    - 约 10 个文件

14. 特性开关 (feature, betas, experiments)
    - 约 10 个文件

15. 自动更新 (autoUpdater)
    - 约 3 个文件

16. 启动 (bootstrap, startup)
    - 约 5 个文件

17. 其他 (abortController, CircularBuffer, which, etc.)
    - 约 40 个文件

总计：约 270 个文件
```
