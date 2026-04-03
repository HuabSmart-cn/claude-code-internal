# ink/hooks

## 功能
React 风格的 Hooks，用于在组件中访问 Ink 框架能力。

## 文件说明

| Hook | 功能 |
|------|------|
| `use-animation-frame.ts` | requestAnimationFrame 替代，用于动画 |
| `use-app.ts` | 访问 App 上下文 |
| `use-declared-cursor.ts` | 声明光标样式 |
| `use-input.ts` | 捕获用户键盘/鼠标输入 |
| `use-interval.ts` | 定时器 hook |
| `use-search-highlight.ts` | 搜索高亮状态 |
| `use-selection.ts` | 文本选择管理 |
| `use-stdin.ts` | 访问标准输入 |
| `use-tab-status.ts` | Tab 键状态 |
| `use-terminal-focus.ts` | 终端聚焦状态 |
| `use-terminal-title.ts` | 设置终端窗口标题 |
| `use-terminal-viewport.ts` | 终端视口信息 |

## 核心概念

### use-input
最常用的 hook，捕获用户交互：
```typescript
useInput((input, key) => {
  if (key.return) handleSubmit()
  if (key.escape) handleCancel()
})
```

### use-animation-frame
替代 `setInterval`，与终端渲染同步的动画帧。

### use-selection
管理文本选择状态，用于支持选择-复制等交互。

### use-terminal-focus
检测终端是否处于活动窗口。
