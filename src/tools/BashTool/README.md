# BashTool

## 功能

执行 shell 命令的核心工具。提供安全沙箱、权限管理和命令验证。

## 核心文件

- `BashTool.tsx` - 主工具实现
- `bashSecurity.ts` - Bash 安全验证
- `bashPermissions.ts` - 权限检查
- `pathValidation.ts` - 路径验证
- `readOnlyValidation.ts` - 只读验证
- `sedValidation.ts` - sed 命令验证
- `commandSemantics.ts` - 命令语义分析
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件
- `utils.ts` - 工具函数
- `bashCommandHelpers.ts` - Bash 命令辅助函数

## 关键类型/函数

```typescript
// 核心输入
interface BashToolInput {
  command: string        // 要执行的命令
  workingDirectory?: string
  timeout?: number        // 超时毫秒
  // ...
}
```

## 安全机制

1. **沙箱模式** (`shouldUseSandbox.ts`) - 是否使用沙箱执行
2. **路径验证** (`pathValidation.ts`) - 验证路径访问权限
3. **只读检查** (`readOnlyValidation.ts`) - 防止写入操作
4. **危险命令警告** - 检测破坏性命令
5. **sed 编辑解析** - 安全处理 sed 命令

## 命令分类 (用于折叠显示)

```typescript
const BASH_SEARCH_COMMANDS = new Set(['find', 'grep', 'rg', 'ag', ...])
const BASH_READ_COMMANDS = new Set(['cat', 'head', 'tail', 'less', ...])
const BASH_LIST_COMMANDS = new Set(['ls', 'tree', 'du'])
```

## 对应命令/用途

BashTool 是 Claude Code 执行系统命令的主要接口，用于：
- 文件操作（ls, cp, mv, rm 等）
- 代码编译和运行
- Git 操作
- 包管理

**重要工具**：最核心的工具之一，几乎所有文件操作和系统交互都依赖它。
