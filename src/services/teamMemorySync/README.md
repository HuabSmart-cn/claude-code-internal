# services/teamMemorySync - 团队记忆同步

## 功能

团队记忆同步服务在多用户间共享项目上下文和记忆。

## 文件列表

| 文件 | 功能 | 大小 |
|------|------|------|
| `index.ts` | 同步核心 | 20KB |
| `securityCheck.tsx` | 安全检查 | 10KB |
| `syncCache.ts` | 同步缓存 | 4KB |
| `syncCacheState.ts` | 缓存状态 | 4KB |
| `types.ts` | 类型定义 | 1KB |

## 同步类型

### 1. 实时同步
```typescript
// 成员 A 的更改立即推送给成员 B
await teamMemory.sync({ type: 'realtime', memory: newMemory })
```

### 2. 定期同步
```typescript
// 每 30 秒同步一次
await teamMemory.sync({ type: 'periodic', interval: 30000 })
```

### 3. 按需同步
```typescript
// 手动触发同步
await teamMemory.sync({ type: 'on-demand' })
```

## 安全机制

### securityCheck.tsx
- 验证用户权限
- 检查敏感数据访问
- 审计日志记录

## 冲突处理

```
成员 A:  Memory_v1
成员 B:  Memory_v1
        ↓
   双向修改
        ↓
   冲突检测
        ↓
   策略选择: Last-Write-Wins / Merge / Manual
```

## 缓存策略

```
Local Cache ← syncCache.ts
     ↓ (miss)
Remote Memory
```
