# Claude Code 源码解析 | Claude Code Source Code Analysis

[中文](#中文版) | [English](#english-version)

---

## 中文版

### 项目简介

本项目对 [Claude Code](https://github.com/anthropics/claude-code) 源码进行逐模块解析，帮助开发者深入理解这个强大 CLI 工具的内部工作机制。

> Claude Code 是 Anthropic 公司开发的命令行编程助手，支持文件读写、命令执行、代码搜索、任务管理、MCP 扩展等功能。

### 源码统计

| 指标 | 数量 |
|------|------|
| 总文件数 | 1902 |
| TypeScript 文件 | ~1900 |
| 代码目录 | 301 |
| 解析文档 | 287 |

### 目录结构

```
claude code 源码解析/
├── README.md                 # 本文件（双语）
├── src/                     # 源码解析文档
│   ├── Task.ts.md          # 任务系统
│   ├── Tool.ts.md          # 工具系统
│   ├── history.ts.md        # 历史记录
│   ├── query.md/           # 查询引擎
│   ├── commands/            # 命令系统 (87)
│   ├── tools/              # 工具实现 (46)
│   ├── components/          # UI组件 (32)
│   ├── hooks/              # React Hooks
│   ├── services/           # 核心服务
│   ├── utils/             # 工具函数 (36)
│   ├── ink/               # 终端UI框架
│   └── ...
```

### 核心模块

| 模块 | 说明 | 文档 |
|------|------|------|
| [tools/](src/tools/README.md) | 45+ 工具实现 | 工具注册、分类、接口 |
| [commands/](src/commands/README.md) | 100+ 命令 | 命令类型、分类、架构 |
| [services/](src/services/README.md) | 核心服务 | API、压缩、MCP |
| [components/](src/components/README.md) | UI 组件 | React 组件、权限对话框 |
| [utils/](src/utils/README.md) | 工具函数 | Git、权限、Shell |
| [ink/](src/ink/README.md) | 终端渲染 | Ink 框架、Box 模型 |

### 快速导航

- [主入口 main.tsx](src/main.tsx.md) - 应用启动入口
- [初始化 setup.ts](src/setup.ts.md) - 环境配置
- [查询引擎 query.ts](src/query.ts.md) - AI 对话核心
- [任务系统 Task.ts](src/Task.ts.md) - 后台任务管理
- [工具系统 Tool.ts](src/Tool.ts.md) - 工具接口定义
- [命令系统 commands.ts](src/commands.ts.md) - 命令注册

### 学习路径

```
1. 入门: main.tsx → setup.ts → commands.ts
2. 核心: query.ts → Tool.ts → Task.ts
3. 扩展: tools/ → commands/ → plugins/
```

### 解析文件列表

| 目录 | 文件数 | 主要内容 |
|------|--------|----------|
| commands/ | 87 | /help, /compact, /review 等命令 |
| tools/ | 46 | Read, Edit, Bash, Grep 等工具 |
| utils/ | 36 | Git、权限、Shell、消息处理 |
| components/ | 32 | UI 组件、权限对话框 |
| query/ | 5 | Token 预算、配置、停止钩子 |
| ink/ | 6 | 终端 UI 框架 |
| vim/ | 5 | Vim 模式实现 |
| upstreamproxy/ | 2 | WebSocket 代理 |

### 如何使用

1. **按模块学习** - 选择感兴趣的核心模块开始
2. **对照源码** - 解析文档配合源码一起阅读
3. **关注类型定义** - TypeScript 类型即最好的文档
4. **运行调试** - 通过 `claude code` 实际运行体验

### 相关资源

- [Claude Code 官方文档](https://docs.anthropic.com/claude-code)
- [Anthropic API 文档](https://docs.anthropic.com/)
- [MCP 协议](https://modelcontextprotocol.io/)

---

## English Version

### Project Overview

This project provides a comprehensive module-by-module analysis of the [Claude Code](https://github.com/anthropics/claude-code) source code, designed to help developers understand the internal architecture of this powerful CLI tool.

> Claude Code is Anthropic's command-line programming assistant, supporting file operations, command execution, code search, task management, and MCP extensions.

### Source Statistics

| Metric | Count |
|--------|-------|
| Total Files | 1902 |
| TypeScript Files | ~1900 |
| Directories | 301 |
| Documentation | 287 |

### Directory Structure

```
claude-code-source-analysis/
├── README.md                 # Bilingual README
├── src/                     # Source analysis docs
│   ├── Task.ts.md          # Task system
│   ├── Tool.ts.md          # Tool system
│   ├── history.ts.md        # History management
│   ├── query.md/           # Query engine
│   ├── commands/            # Commands (87)
│   ├── tools/              # Tools (46)
│   ├── components/          # UI Components (32)
│   ├── hooks/              # React Hooks
│   ├── services/           # Core Services
│   ├── utils/             # Utilities (36)
│   ├── ink/               # Terminal UI Framework
│   └── ...
```

### Core Modules

| Module | Description | Docs |
|--------|-------------|------|
| [tools/](src/tools/README.md) | 45+ tool implementations | Registration, classification, interfaces |
| [commands/](src/commands/README.md) | 100+ commands | Types, classification, architecture |
| [services/](src/services/README.md) | Core services | API, compact, MCP |
| [components/](src/components/README.md) | UI components | React components, permission dialogs |
| [utils/](src/utils/README.md) | Utilities | Git, permissions, shell, messages |
| [ink/](src/ink/README.md) | Terminal renderer | Ink framework, Box model |

### Quick Navigation

- [Entry Point main.tsx](src/main.tsx.md) - Application entry
- [Initialization setup.ts](src/setup.ts.md) - Environment configuration
- [Query Engine query.ts](src/query.ts.md) - AI dialogue core
- [Task System Task.ts](src/Task.ts.md) - Background task management
- [Tool System Tool.ts](src/Tool.ts.md) - Tool interface definition
- [Command System commands.ts](src/commands.ts.md) - Command registration

### Learning Path

```
1. Getting Started: main.tsx → setup.ts → commands.ts
2. Core Concepts: query.ts → Tool.ts → Task.ts
3. Extension: tools/ → commands/ → plugins/
```

### Documentation Files

| Directory | Files | Content |
|----------|-------|---------|
| commands/ | 87 | /help, /compact, /review commands |
| tools/ | 46 | Read, Edit, Bash, Grep tools |
| utils/ | 36 | Git, permissions, shell, messages |
| components/ | 32 | UI components, permission dialogs |
| query/ | 5 | Token budget, config, stop hooks |
| ink/ | 6 | Terminal UI framework |
| vim/ | 5 | Vim mode implementation |
| upstreamproxy/ | 2 | WebSocket proxy |

### How to Use

1. **Learn by Module** - Start with core modules you're interested in
2. **Read with Source** - Use analysis docs alongside original source
3. **Focus on Types** - TypeScript types are the best documentation
4. **Run and Debug** - Experience it firsthand with `claude code`

### Architecture Overview

```
┌─────────────────────────────────────────────────────┐
│                   CLI Entry (main.tsx)              │
└─────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────┐
│              Initialization (setup.ts)              │
└─────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────┐
│            Query Engine (query.ts)                  │
│     User Input → AI Dialog → Tool Call → Output    │
└─────────────────────────────────────────────────────┘
                          │
          ┌───────────────┼───────────────┐
          ▼               ▼               ▼
    ┌──────────┐  ┌──────────┐  ┌──────────┐
    │  Tasks   │  │  Tools   │  │  State   │
    └──────────┘  └──────────┘  └──────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────┐
│                 UI Layer (Ink + React)              │
└─────────────────────────────────────────────────────┘
```

### Related Resources

- [Claude Code Official Docs](https://docs.anthropic.com/claude-code)
- [Anthropic API Docs](https://docs.anthropic.com/)
- [MCP Protocol](https://modelcontextprotocol.io/)

---

## License

本解析项目基于 Claude Code 源码，仅供学习研究使用。

This analysis is based on Claude Code source code, for educational purposes only.

**Analysis Version**: Claude Code v2.1.90
**Analysis Date**: 2026-04-03
