# NotebookEditTool

## 功能

编辑 Jupyter Notebook 文件。

## 核心文件

- `NotebookEditTool.ts` - 主工具实现
- `constants.ts` - 常量定义
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface NotebookEditInput {
  notebook_path: string       // notebook 文件路径
  cell_id?: string           // 要编辑的单元格 ID
  new_source?: string        // 新的单元格内容
  cell_type?: 'code' | 'markdown'  // 单元格类型
  edit_mode?: 'replace' | 'insert' | 'delete'  // 编辑模式
}
```

## 编辑模式

1. **replace** - 替换单元格内容
2. **insert** - 插入新单元格
3. **delete** - 删除单元格

## 对应命令/用途

NotebookEdit 用于交互式编程和数据科学工作流。

**常用场景**：修改 Jupyter notebook、运行数据实验。
