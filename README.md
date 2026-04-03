# Claude Code 源码中文 Wiki

本文件说明：总索引文档，介绍整个 Wiki 的结构和各部分内容。

## 概述

Claude Code 是 Anthropic 开发的 CLI 工具，用于在终端环境中与 Claude 交互完成软件工程任务。本 Wiki 基于 2026-03-31 通过 npm source map 泄露的源码进行详细分析的汇报。

## 源文件项目规模

- **文件数量**：约 1900 个文件
- **代码规模**：512K+ 行代码
- **源码泄露时间**：2026-03-31（通过 npm source map）

## Wiki 结构

本 Wiki 包含以下章节：

1. 架构总览 - Claude Code 整体架构设计
2. 核心模块详解 - main.tsx, QueryEngine, Tool, commands 等核心文件分析
3. 工具系统 - 所有内置工具的实现详解
4. 命令系统 - slash command 系统详解
5. 服务层详解 - API、MCP、OAuth、LSP 等服务
6. 桥接系统 - IDE 桥接和远程控制
7. 权限系统 - 权限控制和安全机制
8. 插件与技能系统 - 扩展机制
9. 状态与任务管理 - 状态系统和任务管理
10. 多智能体协作 - Agent 系统
11. Swarm系统 - 多智能体协作框架
12. UI组件系统 - React/Ink UI 组件
13. 配置与迁移系统 - Zod 配置和迁移
14. 网络与代理 - 代理和远程会话
15. 其他重要模块 - 其他关键模块

## 源码解析

本项目对 Claude Code 源码进行逐模块解析，帮助开发者深入理解这个强大 CLI 工具的内部工作机制。

### 源码统计

| 指标 | 数量 |
|------|------|
| 总文件数 | 1902 |
| TypeScript 文件 | ~1900 |
| 代码目录 | 301 |
| 解析文档 | 287 |

### 核心模块

| 模块 | 说明 | 文档 |
|------|------|------|
| tools/ | 45+ 工具实现 | 工具注册、分类、接口 |
| commands/ | 100+ 命令 | 命令类型、分类、架构 |
| services/ | 核心服务 | API、压缩、MCP |
| components/ | UI 组件 | React 组件、权限对话框 |
| utils/ | 工具函数 | Git、权限、Shell |
| ink/ | 终端渲染 | Ink 框架、Box 模型 |

### 快速导航

- [主入口 main.tsx](src/main.tsx.md) - 应用启动入口
- [初始化 setup.ts](src/setup.ts.md) - 环境配置
- [查询引擎 query.ts](src/query.ts.md) - AI 对话核心
- [任务系统 Task.ts](src/Task.ts.md) - 后台任务管理
- [工具系统 Tool.ts](src/Tool.ts.md) - 工具接口定义
- [命令系统 commands.ts](src/commands.ts.md) - 命令注册

## 免责声明

- 本仓库是**教育和安全性研究文档**，由华彬智融知识数据库维护
- 旨在研究源码暴露、包装失败和现代代理 CLI 系统架构
- Claude Code 原始源码版权归 **Anthropic** 所有，本库不涉及有关内容
- 本仓库**不隶属于、不代表、不受 Anthropic 维护或赞助**

## 华彬智融知识数据库

- 唯一官网：<www.huabsmart.cn>
- 飞书知识库wiki：<https://bl7rsz9526.feishu.cn/wiki/space/7447214332972187650?ccm_open_type=lark_wiki_spaceLink&open_tab_from=wiki_home>
- 飞书官方知识库：<https://www.feishu.cn/community/articleid=7475329207598317569>

**Analysis Version**: Claude Code v2.1.90
**Analysis Date**: 2026-04-03
