# ink.ts

## 文件概述
**路径**: `src/ink.ts`
**功能**: Ink (React for CLI) 渲染层入口，封装 Ink 并集成主题系统
**重要程度**: ★★★★★

---

## 核心概念
### Ink
Ink 是 React 的 CLI 版本，允许使用 React 组件构建交互式命令行界面。

### ThemeProvider
Claude Code 的主题系统包装器，所有渲染调用都通过它包裹。

### 渲染选项
```typescript
type RenderOptions = {
  stdout?: NodeJS.WriteStream
  stderr?: NodeJS.WriteStream
  stdin?: NodeJS.WriteStream
  exitVirtual?: boolean
}
```

---

## 关键函数
```typescript
/**
 * 创建 Ink 根容器
 */
async function createRoot(options?: RenderOptions): Promise<Root>

/**
 * 渲染 React 节点到终端
 */
async function render(
  node: ReactNode,
  options?: NodeJS.WriteStream | RenderOptions
): Promise<Instance>
```

---

## 导出组件
```typescript
// 设计系统
export { ThemeProvider, useTheme, usePreviewTheme, useThemeSetting }
export { color } from './components/design-system/color.js'
export { Box, type BoxProps }
export { Text, type TextProps }

// Ink 组件
export { default as Button }
export { default as Link }
export { default as Newline }
export { NoSelect }
export { RawAnsi }
export { default as Spacer }

// Ink 钩子
export { default as useApp }
export { default as useInput }
export { default as useStdin }
export { useAnimationFrame }
export { useSelection }
export { useTabStatus }
export { useTerminalFocus }
export { useTerminalTitle }
export { useTerminalViewport }
```

---

## 与其他模块的关系
- 调用：`ink/root.js` - 底层 Ink 实现
- 被调用：
  - `main.tsx` - 应用入口
  - `interactiveHelpers.tsx` - 对话框渲染
  - `replLauncher.tsx` - REPL 渲染

---

## 英文对照词汇表
| English | 中文 |
|---------|------|
| Ink | Ink (React for CLI) |
| Render | 渲染 |
| Root | 根容器 |
| Theme | 主题 |
| ThemeProvider | 主题提供者 |
| Component | 组件 |
| Hook | 钩子 |
