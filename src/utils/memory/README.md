# memory/ - 内存管理

## 功能概述

`memory/` 目录管理 Claude Code 的记忆功能。

## 文件列表

```
memory/
├── api.ts               # API
├── environments.ts      # 环境
├── environmentSelection.ts  # 环境选择
└── gitBundle.ts        # Git 捆绑
```

## 记忆类型

### AutoMem
自动记忆功能。

### User Memory
用户定义的记忆。

### Project Memory
项目级记忆。

## 记忆文件

- `CLAUDE.md` - 项目/用户记忆
- `CLAUDE.local.md` - 本地记忆
