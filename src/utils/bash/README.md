# bash/ - Bash 命令解析与执行

## 功能概述

`bash/` 目录负责 Bash 命令的解析、分析和执行相关功能。

## 文件列表

```
bash/
├── ast.ts               # Bash AST（抽象语法树）
├── bashParser.ts        # Bash 解析器
├── bashPipeCommand.ts   # 管道命令处理
├── commands.ts          # 命令定义和处理
├── heredoc.ts          # Here document 处理
├── ParsedCommand.ts     # 解析后命令
├── parser.ts            # 解析器入口
├── prefix.ts            # 前缀处理
├── registry.ts         # 命令注册表
├── shellCompletion.ts   # Shell 补全
├── shellPrefix.ts       # Shell 前缀
├── shellQuote.ts       # Shell 引号处理
├── shellQuoting.ts     # Shell 引用规则
├── ShellSnapshot.ts     # Shell 快照
├── treeSitterAnalysis.ts # Tree-sitter 分析
└── specs/               # 测试规格
```

## 核心功能

### 命令解析
- `parser.ts` - 入口解析器
- `bashParser.ts` - 主要解析器（130KB）
- `ast.ts` - 抽象语法树

### 管道与重定向
- `bashPipeCommand.ts` - 管道命令处理
- `commands.ts` - 命令执行

### Shell 特性
- `heredoc.ts` - Here document 解析
- `shellQuoting.ts` - 引用规则
- `shellQuote.ts` - Shell 引号处理

### 补全
- `shellCompletion.ts` - Shell 补全支持

## 关键模块

### BashParser
```typescript
// 解析 Bash 命令
export function parseBashCommand(input: string): ParsedCommand
```

### ShellSnapshot
保存 Shell 状态快照，用于恢复。
