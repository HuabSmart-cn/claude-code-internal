# ListMcpResourcesTool

## 功能

列出所有已连接的 MCP 服务器提供的资源。

## 核心文件

- `ListMcpResourcesTool.ts` - 主工具实现
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface ListMcpResourcesInput {
  server?: string            // 可选：按服务器过滤
}

interface ListMcpResourcesOutput {
  uri: string
  name: string
  mimeType?: string
  description?: string
  server: string
}[]
```

## 对应命令/用途

ListMcpResourcesTool 用于查看 MCP 服务器提供的可读资源。

**特性**：
- 只读操作
- 延迟加载（shouldDefer: true）
