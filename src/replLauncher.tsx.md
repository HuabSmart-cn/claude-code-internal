# replLauncher.tsx

## 文件概述
**路径**: `src/replLauncher.tsx`
**功能**: REPL (Read-Eval-Print Loop) 的启动器组件
**重要程度**: ★★★★★

---

## 核心概念
### REPL
交互式命令行界面，是 Claude Code 的主要 UI 模式。

### launchRePL
异步函数，负责：
1. 动态导入 App 和 REPL 组件
2. 使用 renderAndRun 渲染完整应用

---

## 关键函数
```typescript
type AppWrapperProps = {
  getFpsMetrics: () => FpsMetrics | undefined
  stats?: StatsStore
  initialState: AppState
}

async function launchRepl(
  root: Root,
  appProps: AppWrapperProps,
  replProps: REPLProps,
  renderAndRun: (root: Root, element: React.ReactNode) => Promise<void>
): Promise<void>
```

---

## 实现
```typescript
async function launchRepl(root, appProps, replProps, renderAndRun) {
  const [{ App }, { REPL }] = await Promise.all([
    import('./components/App.js'),
    import('./screens/REPL.js')
  ])

  await renderAndRun(
    root,
    <App {...appProps}>
      <REPL {...replProps} />
    </App>
  )
}
```

---

## 与其他模块的关系
- 调用：
  - `components/App.js` - 主应用组件
  - `screens/REPL.js` - REPL 屏幕
  - `interactiveHelpers.tsx` - renderAndRun
- 被调用：`main.tsx` - 应用启动

---

## 英文对照词汇表
| English | 中文 |
|---------|------|
| REPL | 交互式解释器 |
| Launcher | 启动器 |
| App | 应用 |
| Render | 渲染 |
