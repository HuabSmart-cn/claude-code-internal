# ReadMcpResourceTool

## 功能

读取 MCP 服务器提供的资源内容。

## 核心文件

- `ReadMcpResourceTool.ts` - 主工具实现
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface ReadMcpResourceInput {
  server: string             // MCP 服务器名称
  uri: string                // 资源 URI
}

interface ReadMcpResourceOutput {
  contents: Array<{
    uri: string
    mimeType?: string
    text?: string
    blobSavedTo?: string     // 二进制内容保存路径
  }>
}
```

## 对应命令/用途

ReadMcpResourceTool 用于读取 MCP 资源的内容。

**特性**：
- 只读操作
- 延迟加载（shouldDefer: true）
