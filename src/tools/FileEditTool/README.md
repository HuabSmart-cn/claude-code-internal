# FileEditTool (Edit)

## 功能

通过 apply patches 方式编辑文件。生成精确的 diff 并应用更改。

## 核心文件

- `FileEditTool.ts` - 主工具实现
- `types.ts` - 类型定义
- `utils.ts` - 工具函数（patch 生成、字符串查找等）
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface FileEditInput {
  file_path: string           // 文件路径
  old_string: string          // 原字符串（精确匹配）
  new_string: string          // 新字符串
  // 或使用 diff
  edits?: [{
    old_string: string
    new_string: string
  }]
}
```

## 编辑模式

1. **字符串替换** - 精确匹配 `old_string` 并替换
2. **多编辑** - 一次性执行多个编辑
3. **Diff 验证** - 确保编辑正确应用

## 特性

- **文件修改时间检查** - 检测意外修改
- **Git Diff 获取** - 显示更改内容
- **路径验证** - 权限检查
- **CLAUDE.md 激活** - 编辑时触发 skills

## 对应命令/用途

Edit 工具用于修改现有文件，是代码修改的主要工具。

**重要工具**：核心编辑工具。
