# SyntheticOutputTool

## 功能

返回结构化输出（JSON 格式）。

## 核心文件

- `SyntheticOutputTool.ts` - 主工具实现

## 关键类型/函数

```typescript
// 允许任意输入（由调用者定义）
const inputSchema = z.object({}).passthrough()
const outputSchema = z.string()
```

## 特性

- **验证输入** - 验证输入是否为有效 JSON
- **直接返回** - 返回输入作为结构化输出
- **仅交互模式** - 仅在非交互会话中启用

## 对应命令/用途

SyntheticOutputTool 用于 SDK/程序化场景返回结构化数据。

**注意**：工具名为 `StructuredOutput`。
