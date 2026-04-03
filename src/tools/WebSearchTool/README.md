# WebSearchTool

## 功能

执行网络搜索。

## 核心文件

- `WebSearchTool.ts` - 主工具实现
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface WebSearchInput {
  query: string                      // 搜索查询
  allowed_domains?: string[]          // 允许的域名
  blocked_domains?: string[]         // 屏蔽的域名
}
```

## 特性

- **域名过滤** - 支持黑白名单
- **流式处理** - 支持进度显示
- **结果缓存** - 避免重复搜索

## 对应命令/用途

WebSearch 用于获取最新信息、研究技术问题。

**常用场景**：查找文档、搜索解决方案。
