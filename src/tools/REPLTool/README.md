# REPLTool

## 功能

提供 REPL（Read-Eval-Print Loop）包装器。

## 核心文件

- `REPLTool.ts` - 主工具实现（仅类型定义）
- `constants.ts` - 常量定义
- `primitiveTools.ts` - 原始工具映射

## 特性

- **工具包装** - 将 Bash/Read/Edit 等工具封装在 REPL VM 中
- **REPL 模式切换** - 隐藏原始工具，仅暴露 REPL

## 对应命令/用途

REPLTool 用于 REPL 模式下的工具管理。

**注意**：这是 Ant-only 工具（`USER_TYPE === 'ant'`）。

**相关工具**：REPL_ONLY_TOOLS 常量定义哪些工具在 REPL 模式下被隐藏。
