# ink/events

## 功能
事件系统，处理终端输入事件的分发和回调。

## 文件说明

| 文件 | 功能 |
|------|------|
| `click-event.ts` | 点击事件定义 |
| `dispatcher.ts` | 事件分发器 |
| `emitter.ts` | 事件发射器 |
| `event-handlers.ts` | 事件处理函数 |
| `event.ts` | 事件基础类型 |
| `focus-event.ts` | 焦点事件 |
| `input-event.ts` | 输入事件 |
| `keyboard-event.ts` | 键盘事件 |
| `terminal-event.ts` | 终端事件 |
| `terminal-focus-event.ts` | 终端焦点事件 |

## 核心概念

### 事件类型
- **KeyboardEvent** - 键盘按键
- **MouseEvent** - 鼠标点击/移动
- **FocusEvent** - 焦点变化
- **TerminalEvent** - 终端特定事件（窗口大小变化等）

### 事件流
1. 终端输入捕获
2. 解析为事件对象
3. 事件分发器路由
4. 组件事件处理

### 事件处理
- `onKeyPress` - 键盘按下
- `onFocus` / `onBlur` - 焦点变化
- `onClick` - 鼠标点击
