# shell/ - Shell 操作

## 功能概述

`shell/` 目录提供跨平台的 Shell 操作支持，包括命令前缀、输出限制和验证。

## 文件列表

```
shell/
├── bashProvider.ts          # Bash 提供商
├── outputLimits.ts          # 输出限制
├── powershellDetection.ts   # PowerShell 检测
├── powershellProvider.ts    # PowerShell 提供商
├── prefix.ts               # 前缀处理
├── readOnlyCommandValidation.ts  # 只读命令验证
├── resolveDefaultShell.ts   # 解析默认 Shell
├── shellProvider.ts        # Shell 提供商
├── shellToolUtils.ts       # Shell 工具函数
└── specPrefix.ts           # Spec 前缀
```

## Shell 类型

```typescript
type ShellType = 'bash' | 'powershell' | 'zsh' | 'fish'
```

## 核心功能

### Shell 检测
`resolveDefaultShell.ts` - 检测系统默认 Shell。

### PowerShell 支持
- `powershellDetection.ts` - 检测 PowerShell
- `powershellProvider.ts` - PowerShell 提供商

### 输出限制
`outputLimits.ts` - 限制命令输出大小。

### 只读命令验证
`readOnlyCommandValidation.ts` - 验证只读命令。

## Shell 提供商

```typescript
interface ShellProvider {
  name: ShellType
  detect(): Promise<boolean>
  getCommandPrefix(): string
  // ...
}
```

## 前缀处理

Shell 命令前缀，用于补全和解析。
