# design-system/

## 功能
设计系统组件库，提供基础 UI 组件和主题系统。

## 组件列表

### 基础组件
- `ThemedText.tsx` - 主题文本组件
- `ThemedBox.tsx` - 主题盒子组件
- `ThemeProvider.tsx` - 主题 Provider（18KB）
- `Tabs.tsx` - 标签页组件（41KB）
- `ListItem.tsx` - 列表项组件（19KB）
- `Pane.tsx` - 面板组件
- `ProgressBar.tsx` - 进度条组件
- `LoadingState.tsx` - 加载状态
- `StatusIcon.tsx` - 状态图标

### 容器组件
- `Dialog.tsx` - 对话框组件（14KB）
- `Divider.tsx` - 分隔线组件
- `KeyboardShortcutHint.tsx` - 快捷键提示
- `Ratchet.tsx` - 棘轮组件

### 选择器组件
- `FuzzyPicker.tsx` - 模糊选择器（40KB）

### 状态组件
- `Byline.tsx` - 描述组件

### 工具
- `color.ts` - 颜色工具

## 重要组件

### ThemeProvider
主题系统核心，提供：
- 亮色/暗色主题切换
- 主题变量注入
- 样式一致性保障

### Tabs
标签页组件，提供：
- 水平/垂直布局
- 可关闭标签
- 动态标签管理

### FuzzyPicker
模糊搜索选择器，用于：
- Agent 选择
- 工具选择
- 快速跳转

### ListItem
统一列表项样式，用于各种列表展示。
