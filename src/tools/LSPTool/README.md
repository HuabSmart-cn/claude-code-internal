# LSPTool

## 功能

与 Language Server Protocol (LSP) 服务器通信，提供代码 intelligence。

## 核心文件

- `LSPTool.ts` - 主工具实现
- `schemas.ts` - 输入模式
- `formatters.ts` - 结果格式化
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface LSPToolInput {
  action: 'goto_definition' | 'find_references' | 'hover' |
          'document_symbol' | 'workspace_symbol' | 'call_hierarchy' |
          'incoming_calls' | 'outgoing_calls'
  path?: string
  // action 特定参数...
}
```

## 支持的 LSP 功能

- **goto_definition** - 跳转到定义
- **find_references** - 查找引用
- **hover** - 悬停信息
- **document_symbol** - 文档符号
- **workspace_symbol** - 工作区符号搜索
- **call_hierarchy** - 调用层次结构

## 对应命令/用途

LSPTool 用于提供 IDE 级别的代码智能功能。

**条件**：仅在 `ENABLE_LSP_TOOL` 环境变量设置时可用。
