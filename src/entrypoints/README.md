# entrypoints

## 功能
程序入口点模块，定义不同的启动入口和 SDK 类型。

## 文件/子目录

### 核心文件
- `agentSdkTypes.ts` - Agent SDK 类型 (13KB)
- `cli.tsx` - CLI 入口 (39KB)
- `init.ts` - 初始化逻辑 (13KB)
- `mcp.ts` - MCP 入口 (6KB)
- `sandboxTypes.ts` - 沙箱类型
- `sdk/` - SDK 子目录

### entrypoints/sdk/ - SDK 定义
- `controlSchemas.ts` - 控制 schema (19KB)
- `coreSchemas.ts` - 核心 schema (56KB)
- `coreTypes.ts` - 核心类型

## 核心概念

### 多入口点
Claude Code 支持多种启动方式：

1. **CLI 入口** (`cli.tsx`)
   - 交互式命令行界面
   - 终端 REPL

2. **MCP 入口** (`mcp.ts`)
   - Model Context Protocol 服务器模式
   - 作为其他工具的 AI 后端

3. **SDK 入口** (`sdk/`)
   - 供外部程序调用的 SDK
   - 核心类型和 Schema 定义

### SDK 类型系统
- `coreTypes.ts` - 核心数据类型
- `coreSchemas.ts` - 核心数据 Schema（Zod 或类似验证）
- `controlSchemas.ts` - 控制指令 Schema

### 沙箱模式
`sandboxTypes.ts` 定义沙箱环境下的类型约束。
