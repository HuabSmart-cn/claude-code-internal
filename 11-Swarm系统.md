# Swarm 系统

## 1. Swarm 系统概述

Swarm 系统是一个多智能体协作框架，支持团队模式、进程内队友和多种终端后端实现。

## 2. 团队模式快照

### 模式类型

| 模式 | 描述 |
|------|------|
| auto | 自动检测可用后端 |
| tmux | 强制使用 Tmux 后端 |
| in-process | 使用进程内后端 |

## 3. 团队辅助函数

- getTeamDir - 获取团队目录
- readTeamFile - 读取团队文件
- removeTeammateFromTeamFile - 移除队友
- setMemberMode - 设置成员权限模式

## 4. 后端系统 (backends/)

### 4.1 后端类型

- TmuxBackend - 使用 tmux 进行面板管理
- ITermBackend - 使用 iTerm2 原生分割面板
- InProcessBackend - 在当前进程中运行队友

### 4.2 PaneBackend 接口

提供 createTeammatePane、sendCommandToPane、setPaneBorderColor、killPane 等方法。

## 5. 权限同步

### 权限请求流程

```
Worker Agent → 权限请求 → Leader Mailbox
Leader Agent ← 轮询 ← 权限队列
     ↓
用户批准/拒绝
     ↓
Leader → 权限响应 → Worker Mailbox
```

## 6. 重连机制

从会话恢复团队上下文，支持重新连接和状态恢复。

## 7. 消息类型

```typescript
export type TeammateMessage = {
  text: string
  from: string
  color?: string
  timestamp?: string
  summary?: string
}
```
