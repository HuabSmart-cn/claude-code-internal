# ink

## 功能
终端 UI 框架，类似 React 但专为终端环境设计，提供声明式组件化界面开发能力。

## 文件/子目录

### 核心文件
- `ink.tsx` - 主入口文件，核心渲染引擎 (251KB)
- `Ansi.tsx` - ANSI 转义序列处理
- `bidi.ts` - 双向文本支持
- `clearTerminal.ts` - 终端清屏功能
- `colorize.ts` - 文本着色
- `dom.ts` - DOM 相关功能
- `focus.ts` - 焦点管理
- `frame.ts` - 边框渲染
- `get-max-width.ts` - 最大宽度计算
- `hit-test.ts` - 点击测试
- `instances.ts` - 实例管理
- `line-width-cache.ts` - 行宽缓存
- `log-update.ts` - 日志更新
- `measure-element.ts` - 元素测量
- `measure-text.ts` - 文本测量
- `node-cache.ts` - 节点缓存
- `optimizer.ts` - 优化器
- `output.ts` - 输出处理
- `parse-keypress.ts` - 键位解析
- `reconciler.ts` - 调和器
- `render-border.ts` - 边框渲染
- `render-node-to-output.ts` - 节点渲染到输出
- `render-to-screen.ts` - 渲染到屏幕
- `renderer.ts` - 渲染器
- `root.ts` - 根节点
- `screen.ts` - 屏幕管理
- `searchHighlight.ts` - 搜索高亮
- `selection.ts` - 选择管理
- `squash-text-nodes.ts` - 文本节点压缩
- `stringWidth.ts` - 字符串宽度
- `styles.ts` - 样式处理
- `supports-hyperlinks.ts` - 超链接支持
- `tabstops.ts` - 制表位
- `terminal-focus-state.ts` - 终端焦点状态
- `terminal-querier.ts` - 终端查询
- `terminal.ts` - 终端
- `termio.ts` - 终端 IO 入口
- `useTerminalNotification.ts` - 终端通知
- `warn.ts` - 警告
- `widest-line.ts` - 最宽行
- `wrap-text.ts` - 文本换行
- `wrapAnsi.ts` - ANSI 换行
- `constants.ts` - 常量

### ink/components/ - UI 组件
- `AlternateScreen.tsx` - 交替屏幕
- `App.tsx` - 应用组件 (主组件)
- `AppContext.ts` - 应用上下文
- `Box.tsx` - 盒容器组件
- `Button.tsx` - 按钮组件
- `ClockContext.tsx` - 时钟上下文
- `CursorDeclarationContext.ts` - 光标声明上下文
- `ErrorOverview.tsx` - 错误概览
- `Link.tsx` - 链接组件
- `Newline.tsx` - 换行组件
- `NoSelect.tsx` - 禁用选择组件
- `RawAnsi.tsx` - 原始 ANSI
- `ScrollBox.tsx` - 滚动盒
- `Spacer.tsx` - 空格组件
- `StdinContext.ts` - 标准输入上下文
- `TerminalFocusContext.tsx` - 终端焦点上下文
- `TerminalSizeContext.tsx` - 终端大小上下文
- `Text.tsx` - 文本组件

### ink/events/ - 事件处理
- `click-event.ts` - 点击事件
- `dispatcher.ts` - 事件分发
- `emitter.ts` - 事件发射
- `event-handlers.ts` - 事件处理
- `event.ts` - 事件基础
- `focus-event.ts` - 焦点事件
- `input-event.ts` - 输入事件
- `keyboard-event.ts` - 键盘事件
- `terminal-event.ts` - 终端事件
- `terminal-focus-event.ts` - 终端焦点事件

### ink/hooks/ - React 风格 Hooks
- `use-animation-frame.ts` - 动画帧
- `use-app.ts` - 应用 hook
- `use-declared-cursor.ts` - 声明光标
- `use-input.ts` - 输入 hook
- `use-interval.ts` - 间隔 hook
- `use-search-highlight.ts` - 搜索高亮
- `use-selection.ts` - 选择 hook
- `use-stdin.ts` - 标准输入
- `use-tab-status.ts` - Tab 状态
- `use-terminal-focus.ts` - 终端焦点
- `use-terminal-title.ts` - 终端标题
- `use-terminal-viewport.ts` - 终端视口

### ink/layout/ - 布局引擎
- `engine.ts` - Yoga 布局引擎封装
- `geometry.ts` - 几何计算
- `node.ts` - 布局节点
- `yoga.ts` - Yoga 布局库

### ink/termio/ - 终端 IO
- `ansi.ts` - ANSI 序列
- `csi.ts` - CSI 序列
- `dec.ts` - DEC 序列
- `esc.ts` - ESC 序列
- `osc.ts` - OSC 序列
- `parser.ts` - 解析器
- `sgr.ts` - SGR 序列
- `tokenize.ts` - 分词
- `types.ts` - 类型定义

## 核心概念

### 声明式 UI
Ink 采用类似 React 的声明式 UI 范式，使用 JSX 语法描述终端界面。

### 组件系统
- **Box**: 基础容器组件，支持 flexbox 布局
- **Text**: 文本显示组件，支持样式
- **Button**: 交互按钮组件
- **ScrollBox**: 滚动容器

### Yoga 布局引擎
使用 Facebook 的 Yoga 布局引擎实现灵活的 flexbox 布局。

### 事件处理
- 键盘事件：按键捕获和分发
- 焦点事件：组件焦点管理
- 输入事件：用户输入处理
- 点击事件：鼠标/点击支持

### ANSI 转义序列
完整支持 ANSI 转义序列用于颜色、样式、光标控制等。

### 渲染流程
1. 组件树构建 (JSX)
2. 布局计算 (Yoga)
3. 调和比对 (Reconciler)
4. 输出渲染 (render-to-screen)
