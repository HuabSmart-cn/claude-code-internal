# FileReadTool (Read)

## 功能

读取文件内容，支持普通文本、PDF、Jupyter Notebook 和图片处理。

## 核心文件

- `FileReadTool.ts` - 主工具实现
- `limits.ts` - 读取限制配置
- `imageProcessor.ts` - 图片处理
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface FileReadInput {
  file_path: string           // 文件路径
  offset?: number              // 起始行
  limit?: number              // 行数限制
  show_line_numbers?: boolean  // 显示行号
  // PDF 特定参数
  pages?: string               // 页码范围 "1-5, 10"
}
```

## 支持的文件格式

1. **普通文本** - 直接读取，带语法高亮
2. **PDF** - 提取文本内容或页面
3. **Jupyter Notebook** - 解析单元格
4. **图片** - 调整大小、生成元数据

## 特性

- **行范围读取** - 支持 offset + limit
- **Token 限制** - 自动估算和限制
- **自动记忆刷新** - 触发相关 skills
- **二进制检测** - 拒绝或特殊处理二进制文件

## 对应命令/用途

Read 工具用于查看文件内容，是代码分析和理解的基础。

**重要工具**：最常用的读取工具。
