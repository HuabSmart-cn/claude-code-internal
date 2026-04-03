# PowerShellTool

## 功能

在 Windows 环境下执行 PowerShell 命令。

## 核心文件

- `PowerShellTool.tsx` - 主工具实现
- `toolName.ts` - 工具名称
- `prompt.ts` - 提示词
- `powershellSecurity.ts` - PowerShell 安全验证
- `powershellPermissions.ts` - 权限检查
- `pathValidation.ts` - 路径验证
- `readOnlyValidation.ts` - 只读验证
- `commonParameters.ts` - 通用参数
- `commandSemantics.ts` - 命令语义
- `gitSafety.ts` - Git 安全
- `UI.tsx` - 渲染组件

## 对应命令/用途

PowerShellTool 是 BashTool 在 Windows 上的替代方案。

**条件**：仅在 `isPowerShellToolEnabled()` 时可用。
