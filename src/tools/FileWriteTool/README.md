# FileWriteTool (Write)

## 功能

创建新文件或覆盖现有文件内容。

## 核心文件

- `FileWriteTool.ts` - 主工具实现
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface FileWriteInput {
  file_path: string           // 文件路径
  content: string            // 文件内容
  append?: boolean           // 追加模式（而非覆盖）
}
```

## 特性

- **目录创建** - 自动创建父目录
- **权限检查** - 验证写入权限
- **追加模式** - 支持追加而非覆盖
- **文件历史跟踪** - 记录文件更改

## 对应命令/用途

Write 工具用于创建新文件或完全覆盖文件内容。

**重要工具**：用于文件创建和覆盖。
