# Claude Code Components

## Overview

Claude Code 的 `components` 目录包含 **113+ 个 React 组件**，构成整个应用的 UI 层。这些组件负责：
- 消息渲染（对话界面）
- 权限管理（各种权限请求对话框）
- Agent 管理（创建、编辑、选择 Agent）
- 设置界面（应用配置、Usage 统计）
- MCP 服务器管理
- 任务和后台进程展示
- 设计系统和基础 UI 组件

## Directory Structure

```
components/
├── agents/                    # Agent 管理相关
│   ├── new-agent-creation/     # Agent 创建向导
│   │   └── wizard-steps/        # 向导步骤组件
│   └── ...                      # Agent 选择、编辑组件
├── messages/                   # 消息渲染（核心 UI）
│   └── UserToolResultMessage/   # 工具结果消息
├── permissions/                 # 权限请求系统
│   ├── rules/                   # 权限规则管理
│   └── ...                      # 各种权限请求对话框
├── mcp/                        # MCP 服务器管理 UI
├── Settings/                   # 应用设置界面
├── tasks/                      # 任务和后台进程 UI
├── design-system/              # 设计系统组件
├── ui/                        # 基础 UI 组件
├── PromptInput/               # 提示词输入框
├── skills/                    # Skill 相关 UI
├── shell/                     # Shell 输出展示
├── memory/                    # 记忆功能 UI
├── hooks/                    # React Hooks
├── diff/                     # Diff 展示组件
├── Spinner/                  # 加载动画组件
├── teams/                    # 团队协作 UI
└── [其他组件文件]              # 主目录下的独立组件
```

## Component Categories

| Category | Location | Description |
|----------|----------|-------------|
| **Messages** | `messages/` | 对话消息渲染，包括用户消息、助手消息、工具结果等 |
| **Permissions** | `permissions/` | 权限请求对话框（Bash、File、Network 等） |
| **Agents** | `agents/` | Agent 的创建、编辑、选择、列表管理 |
| **Tasks** | `tasks/` | 后台任务、远程会话、Shell 进度展示 |
| **Settings** | `Settings/` | 应用配置、状态、Usage 统计 |
| **MCP** | `mcp/` | MCP 服务器的连接、配置、管理 |
| **Design System** | `design-system/`, `ui/` | 基础 UI 组件（Tabs、ListItem、Theme 等） |
| **PromptInput** | `PromptInput/` | 提示词输入框及相关组件 |
| **Skills** | `skills/` | Skill 菜单和选择界面 |
| **Shell** | `shell/` | 终端输出、行显示、时间展示 |

## Key Component Files (Root)

| File | Purpose |
|------|---------|
| `App.tsx` | 顶层应用组件，提供 Context .Provider |
| `FullscreenLayout.tsx` | 全屏布局容器 |
| `StatusLine.tsx` | 状态栏组件 |
| `PromptInput.tsx` | 核心输入框组件（355KB，包含输入逻辑） |
| `ContextVisualization.tsx` | 上下文可视化 |
| `Feedback.tsx` | 反馈组件 |
| `GlobalSearchDialog.tsx` | 全局搜索对话框 |
| `HistorySearchDialog.tsx` | 历史搜索对话框 |
| `AutoUpdater.tsx` | 自动更新组件 |
| `ConsoleOAuthFlow.tsx` | OAuth 流程组件 |
| `BridgeDialog.tsx` | Bridge 对话框 |

## State Management Pattern

组件使用 React Context 进行状态管理：
- `AppStateContext` - 应用状态
- `StatsContext` - 统计信息
- `FpsMetricsContext` - FPS 指标

## Component Architecture Notes

1. **消息渲染** (`messages/`) 采用策略模式，不同类型消息有对应的渲染组件
2. **权限系统** (`permissions/`) 是对话式 UI 的核心，请求用户授权操作
3. **Agent 系统** (`agents/`) 支持完整的 CRUD 操作
4. **MCP** (`mcp/`) 提供服务器管理和工具浏览功能
5. **PromptInput** 是最大最复杂的组件，负责用户输入处理
