# GlobTool

## 功能

通过 glob 模式匹配文件名，如 `**/*.ts`、`src/**/*.js`。

## 核心文件

- `GlobTool.ts` - 主工具实现
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface GlobInput {
  pattern: string            // glob 模式
  path?: string              // 搜索目录（默认 cwd）
}
```

## 特性

- **结果限制** - 默认限制 100 个文件
- **权限检查** - 验证路径访问权限
- **忽略模式** - 支持忽略特定模式

## 对应命令/用途

Glob 工具用于快速查找匹配特定模式的文件，是代码搜索的基础工具。

**常用场景**：查找特定类型的文件、批量操作。
