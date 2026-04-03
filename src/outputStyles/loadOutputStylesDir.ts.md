# loadOutputStylesDir.ts - 输出样式目录加载

## 文件概述
**路径**: `src/outputStyles/loadOutputStylesDir.ts`
**功能**: 从项目目录和用户目录的 `.claude/output-styles` 目录加载 Markdown 文件作为输出样式

---

## 核心概念
- **输出样式（Output Style）**: 用户定义的 Markdown 格式提示词模板
- **样式源**: 分为项目级样式和用户级样式（用户目录优先级更高）
- **前端matter 元数据**: 样式配置（名称、描述）存储在 Markdown 文件的 frontmatter 中
- **keep-coding-instructions**: 控制是否保留编码指令的标志

## 关键类型/接口
```typescript
// 输出样式配置
type OutputStyleConfig = {
  name: string
  description: string
  prompt: string
  source: string
  keepCodingInstructions?: boolean
}
```

## 核心函数

```typescript
/**
 * 加载输出样式目录中的所有样式
 * 从 .claude/output-styles/*.md 文件读取并解析
 */
export const getOutputStyleDirStyles = memoize(
  async (cwd: string): Promise<OutputStyleConfig[]>
)

/**
 * 清除所有输出样式相关缓存
 */
export function clearOutputStyleCaches(): void
```

## 加载流程
1. 调用 `loadMarkdownFilesForSubdir('output-styles', cwd)` 加载所有 Markdown 文件
2. 对每个文件提取：
   - **文件名** → 样式名称（去掉 `.md` 后缀）
   - **frontmatter.name** → 覆盖默认名称
   - **frontmatter.description** → 样式描述
   - **文件内容** → prompt 提示词
3. 解析 `keep-coding-instructions` 标志
4. 过滤无效样式并返回

## 中英对照
| English | 中文 |
|---------|------|
| Output Style | 输出样式 |
| Output Styles Directory | 输出样式目录 |
| Markdown Files | Markdown 文件 |
| Frontmatter | 前端matter 元数据 |
| Style Name | 样式名称 |
| Style Description | 样式描述 |
| Prompt | 提示词 |
| Keep Coding Instructions | 保留编码指令 |
| Project Styles | 项目样式 |
| User Styles | 用户样式 |
| Source | 来源 |
