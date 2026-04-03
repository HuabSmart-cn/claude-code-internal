# ToolSearchTool

## 功能

搜索延迟加载的工具。

## 核心文件

- `ToolSearchTool.ts` - 主工具实现
- `constants.ts` - 常量定义
- `prompt.ts` - 提示词

## 关键类型/函数

```typescript
interface ToolSearchInput {
  query: string              // 搜索查询
  max_results?: number       // 最大结果数（默认 5）
}

interface ToolSearchOutput {
  matches: string[]          // 匹配的工具名
  query: string
  total_deferred_tools: number
  pending_mcp_servers?: string[]
}
```

## 特性

- **关键字搜索** - 通过 searchHint 匹配
- **直接选择** - 支持 `select:<tool_name>` 格式
- **结果缓存** - 跟踪缓存键变化

## 对应命令/用途

ToolSearchTool 用于在 Tool Deferral 模式下找到并加载工具。

**注意**：仅在 `isToolSearchEnabledOptimistic()` 时可能包含在工具列表中。
