# powershell/ - PowerShell 支持

## 功能概述

`powershell/` 目录提供 PowerShell 命令的解析和执行支持。

## 文件列表

```
powershell/
├── ccrSession.ts       # CCR 会话
├── dangerousCmdlets.ts # 危险 Cmdlet 检测
├── keyword.ts         # 关键字
├── parser.ts          # 解析器 (66KB)
└── staticPrefix.ts   # 静态前缀
```

## 功能

### 解析
`parser.ts` - PowerShell 脚本解析。

### 安全
`dangerousCmdlets.ts` - 检测危险的 PowerShell 命令。
