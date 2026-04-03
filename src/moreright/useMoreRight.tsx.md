# useMoreRight.tsx - 外部构建存根

## 文件概述
**路径**: `src/moreright/useMoreRight.tsx`
**功能**: 外部构建的存根文件，提供空的 useMoreRight hook 实现

---

## 核心概念
- **外部构建存根**: 此文件是外部构建使用的占位符，真正的实现在内部
- **自包含设计**: 不使用相对导入，类型检查时通过 `scripts/external-stubs/src/moreright/` 路径解析
- **无操作实现**: 所有回调返回默认值，不执行任何实际操作

## 关键类型/接口
```typescript
// Hook 参数类型
type M = any

type UseMoreRightArgs = {
  enabled: boolean
  setMessages: (action: M[] | ((prev: M[]) => M[])) => void
  inputValue: string
  setInputValue: (s: string) => void
  setToolJSX: (args: M) => void
}

// Hook 返回类型
type UseMoreRightResult = {
  onBeforeQuery: (input: string, all: M[], n: number) => Promise<boolean>
  onTurnComplete: (all: M[], aborted: boolean) => Promise<void>
  render: () => null
}
```

## 核心函数

```typescript
/**
 * useMoreRight hook - 外部构建返回空实现
 * 内部真实实现在 src/moreright/useMoreRight.ts
 */
export function useMoreRight(_args: UseMoreRightArgs): UseMoreRightResult {
  return {
    onBeforeQuery: async () => true,
    onTurnComplete: async () => {},
    render: () => null
  }
}
```

## 中英对照
| English | 中文 |
|---------|------|
| External Build Stub | 外部构建存根 |
| Hook | 钩子 |
| Query | 查询 |
| Turn Complete | 回合完成 |
| Render | 渲染 |
| Enabled | 启用 |
| Messages | 消息 |
| Input Value | 输入值 |
| Tool JSX | 工具 JSX |
