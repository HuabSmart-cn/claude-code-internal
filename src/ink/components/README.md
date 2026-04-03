# ink/components

## 功能
Ink 终端 UI 框架的核心组件库。

## 文件说明

| 文件 | 功能 |
|------|------|
| `AlternateScreen.tsx` | 切换到备用屏幕缓冲区 |
| `App.tsx` | 主应用组件 (98KB) |
| `AppContext.ts` | 应用上下文 |
| `Box.tsx` | 基础 flexbox 容器 |
| `Button.tsx` | 可交互按钮 |
| `ClockContext.tsx` | 时钟/时间上下文 |
| `CursorDeclarationContext.ts` | 光标声明上下文 |
| `ErrorOverview.tsx` | 错误信息展示 |
| `Link.tsx` | 可点击链接 |
| `Newline.tsx` | 换行符组件 |
| `NoSelect.tsx` | 禁用文本选择 |
| `RawAnsi.tsx` | 原始 ANSI 输出 |
| `ScrollBox.tsx` | 可滚动容器 |
| `Spacer.tsx` | 弹性空格 |
| `StdinContext.ts` | 标准输入上下文 |
| `TerminalFocusContext.tsx` | 终端焦点管理 |
| `TerminalSizeContext.tsx` | 终端尺寸上下文 |
| `Text.tsx` | 文本显示组件 |

## 核心概念

### Box
基础布局组件，封装了 Yoga flexbox 布局引擎：
- 支持 `flexDirection`, `justifyContent`, `alignItems` 等属性
- 支持 `width`, `height`, `margin`, `padding`

### Text
文本渲染组件：
- 支持 `bold`, `italic`, `dim` 等样式
- 支持前景/背景颜色
- 支持嵌套样式

### Button
交互组件：
- 支持 `onPress` 回调
- 支持聚焦状态
- 键盘可访问

### ScrollBox
滚动容器：
- 水平/垂直滚动
- 滚动条显示
- 滚动位置控制

### Context Providers
- `AppContext` - 全局应用状态
- `TerminalFocusContext` - 焦点管理
- `TerminalSizeContext` - 终端尺寸
- `ClockContext` - 时间/时钟
- `StdinContext` - 用户输入
