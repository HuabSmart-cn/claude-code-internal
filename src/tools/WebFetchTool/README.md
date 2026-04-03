# WebFetchTool

## 功能

获取网页内容并使用 AI 处理。

## 核心文件

- `WebFetchTool.ts` - 主工具实现
- `utils.ts` - URL 处理和 markdown 转换
- `preapproved.ts` - 预批准域名
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface WebFetchInput {
  url: string               // 要获取的 URL
  prompt: string            // 对内容处理的提示
}
```

## 特性

- **Markdown 转换** - 将 HTML 转为 Markdown
- **预批准域名** - 避免重复确认
- **内容大小限制** - 防止过大响应
- **错误处理** - 处理 HTTP 错误

## 对应命令/用途

WebFetch 用于获取和分析网页内容，如文档、博客文章等。

**常用场景**：获取 API 文档、阅读网页文章。
