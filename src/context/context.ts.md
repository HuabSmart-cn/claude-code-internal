# context.ts - 上下文管理

## 文件概述
**路径**: `src/context.ts`
**功能**: 管理 Claude Code 的上下文信息，包括 Git 状态、用户上下文、CLAUDE.md 内容等

---

## 核心概念

### 用户上下文 (User Context)
```
Claude Code 在每次对话开始时收集项目上下文信息
包括：
- Git 状态（分支、提交、用户）
- CLAUDE.md 内容
- 项目信息
```

### 系统上下文注入
```
上下文信息会被注入到系统提示中
帮助 Claude 了解项目状态
```

### 缓存管理
```
使用 memoize 缓存上下文
支持缓存清除（当 CLAUDE.md 变化时）
```

---

## 主要函数

### Git 状态
```typescript
/**
 * 获取 Git 状态信息
 * 包括：分支名、默认分支、status、最近5条提交、用户名
 * 状态超过 2000 字符会截断
 */
getGitStatus(): Promise<string | null>
```

### 用户上下文
```typescript
/**
 * 获取用户上下文（memoized）
 * 包含：
 * - Git 状态
 * - CLAUDE.md 内容
 * - 项目路径
 */
getUserContext(): Promise<string>
```

### 系统上下文
```typescript
/**
 * 获取系统上下文
 * 包括：
 * - 日期
 * - 工作目录
 */
getSystemContext(): Promise<string>
```

### CLAUDE.md 管理
```typescript
/**
 * 获取所有 CLAUDE.md 文件
 * 包括项目级和用户级
 */
getClaudeMds(): Promise<ClaudeMd[]>
```

---

## 上下文来源

| 来源 | 说明 |
|------|------|
| Git Status | 分支、提交、用户 |
| CLAUDE.md | 项目说明文件 |
| System Info | 日期、路径 |
| Memory | 记忆文件 |

---

## 英文对照

| English | 中文 |
|---------|------|
| Context | 上下文 |
| User Context | 用户上下文 |
| System Context | 系统上下文 |
| Git Status | Git 状态 |
| Branch | 分支 |
| Commit | 提交 |
| Memory | 记忆 |
| Injection | 注入 |
| Memoize | 记忆化 |
