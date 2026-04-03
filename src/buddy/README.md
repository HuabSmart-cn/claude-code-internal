# buddy - 伙伴模式

## 目录概述
**路径**: `src/buddy/`
**功能**: Claude Code 的伙伴/伴侣模式，提供辅助 AI 角色

---

## 文件列表

| 文件 | 功能 |
|------|------|
| `CompanionSprite.tsx` | 伙伴精灵组件 - 主要的 UI 组件 |
| `companion.ts` | 伙伴实例管理 |
| `types.ts` | 伙伴相关类型定义 |
| `useBuddyNotification.tsx` | 伙伴通知 Hook |
| `prompt.ts` | 伙伴提示词 |
| `sprites.ts` | 精灵/形象定义 |

---

## 核心概念

### 伙伴模式 (Buddy Mode)
```
Buddy 是一个辅助 AI 角色
可以在 Claude Code 中提供额外的帮助和指导
类似于一个虚拟的伴侣/助手
```

### 精灵 (Sprite)
```
Buddy 的视觉形象
通过 sprites.ts 定义
CompanionSprite.tsx 负责渲染
```

### 通知系统
```
通过 useBuddyNotification 管理
Buddy 可以在特定事件发生时提醒用户
```

---

## 主要组件

### CompanionSprite.tsx
```typescript
/**
 * Buddy 的主要视觉组件
 * 渲染伙伴的形象
 */
```

### useBuddyNotification
```typescript
/**
 * 管理伙伴通知的 Hook
 * 处理通知的显示和交互
 */
```

---

## 英文对照

| English | 中文 |
|---------|------|
| Buddy | 伙伴/伴侣 |
| Companion | 伴侣/伙伴 |
| Sprite | 精灵/形象 |
| Notification | 通知 |
| Prompt | 提示词 |
