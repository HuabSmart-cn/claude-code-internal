# processUserInput/ - 用户输入处理

## 功能概述

`processUserInput/` 目录处理用户输入的解析和执行。

## 文件列表

```
processUserInput/
├── processBashCommand.tsx   # 处理 Bash 命令 (22KB)
├── processSlashCommand.tsx  # 处理斜杠命令 (144KB)
├── processTextPrompt.ts     # 处理文本提示
└── processUserInput.ts      # 处理用户输入 (19KB)
```

## 功能

### Slash 命令
`processSlashCommand.tsx` - 处理 `/` 开头的命令（如 `/help`, `/compact`）。

### Bash 命令
`processBashCommand.tsx` - 处理 Bash 命令输入。

### 文本提示
`processTextPrompt.ts` - 处理普通文本输入。
