# GrepTool

## 功能

在文件内容中搜索正则表达式模式。

## 核心文件

- `GrepTool.ts` - 主工具实现
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface GrepInput {
  pattern: string             // 正则表达式
  path?: string               // 搜索路径
  glob?: string               // 文件过滤模式
  output_mode?: 'content' | 'files_with_matches' | 'count'
  '-n'?: boolean              // 显示行号
  '-C'?: number               // 上下文行数
  '-B'?: number               // 匹配前行数
  '-A'?: number               // 匹配后行数
  head_limit?: number         // 结果限制
}
```

## 特性

- **多输出模式** - content、files_with_matches、count
- **上下文支持** - 显示匹配周围的代码
- **文件过滤** - 支持 glob 模式
- **嵌入式搜索** - 当有嵌入工具时跳过此工具

## 对应命令/用途

Grep 是代码搜索的核心工具，用于查找函数调用、变量使用等。

**常用场景**：搜索代码模式、查找字符串。
