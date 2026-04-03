# textObjects.ts - Vim 文本对象查找

## 文件概述
**路径**: `src/vim/textObjects.ts`
**功能**: 实现 Vim 文本对象（word、quote、bracket）的边界查找算法

---

## 核心概念
- **文本对象（Text Object）**: 由分隔符界定的文本区域，如 `iw`（内词）、`a"`（一对引号）
- **inner vs around**: `inner` 仅包含内容，`around` 包含分隔符本身
- **图素安全（Grapheme-safe）**: 使用 Unicode 图素分割器确保正确处理多字节字符
- **配对引号**: 正确处理嵌套引号（如 `"foo "bar" baz"`）

## 关键类型/接口
```typescript
type TextObjectRange = { start: number; end: number } | null
```

## 分隔符配对表
```typescript
const PAIRS: Record<string, [string, string]> = {
  '(': ['(', ')'],   ')': ['(', ')'],
  b: ['(', ')'],     // parenthesis alias
  '[': ['[', ']'],   ']': ['[', ']'],
  '{': ['{', '}'],   '}': ['{', '}'],
  B: ['{', '}'],     // brace alias
  '<': ['<', '>'],   '>': ['<', '>'],
  '"': ['"', '"'],
  "'": ["'", "'"],
  '`': ['`', '`'],
}
```

## 核心函数

```typescript
/**
 * 在指定位置查找文本对象
 */
export function findTextObject(
  text: string,
  offset: number,
  objectType: string,
  isInner: boolean,
): TextObjectRange
```

### 内部实现函数

```typescript
/**
 * 查找词对象（word/WORD）
 */
function findWordObject(
  text: string,
  offset: number,
  isInner: boolean,
  isWordChar: (ch: string) => boolean,
): TextObjectRange

/**
 * 查找引号对象（"、"、"）
 */
function findQuoteObject(
  text: string,
  offset: number,
  quote: string,
  isInner: boolean,
): TextObjectRange

/**
 * 查找括号对象（()、[]、{}、<>）
 */
function findBracketObject(
  text: string,
  offset: number,
  open: string,
  close: string,
  isInner: boolean,
): TextObjectRange
```

## 文本对象类型

| 对象 | 类型 | 说明 |
|------|------|------|
| `iw` | inner word | 内词（不包括周围空白） |
| `aw` | around word | 词（包括前导空白） |
| `iW` | inner WORD | 内 WORD |
| `aW` | around WORD | 外 WORD |
| `i"` | inner double quote | 引号内内容 |
| `a"` | around double quote | 包括引号 |
| `i'` | inner single quote | 单引号内内容 |
| `a'` | around single quote | 包括单引号 |
| `i`` | inner backquote | 反引号内内容 |
| `i(` / `ib` | inner paren | 括号内内容 |
| `a(` / `ab` | around paren | 包括括号 |
| `i[` | inner bracket | 方括号内内容 |
| `a[` | around bracket | 包括方括号 |
| `i{` / `iB` | inner brace | 花括号内内容 |
| `a{` / `aB` | around brace | 包括花括号 |
| `i<` | inner angle | 尖括号内内容 |
| `a<` | around angle | 包括尖括号 |

## 查找算法细节

### 词对象
1. 使用 `getGraphemeSegmenter()` 预分割文本为图素
2. 定位 offset 所在的图素索引
3. 根据图素类型（词/空白/标点）扩展边界
4. 处理 `around` 时包含周围空白

### 引号对象
1. 限制在同一行内查找（Vim 行为）
2. 收集所有引号位置
3. 配对引号（0-1, 2-3, ...）
4. 确定 offset 是否在某个配对内

### 括号对象
1. 从 offset 向左查找开括号，深度计数
2. 从开括号位置向右查找闭括号
3. 返回完整范围

## 中英对照
| English | 中文 |
|---------|------|
| Text Object | 文本对象 |
| Inner | 内部 |
| Around | 周围 |
| Word | 词 |
| WORD | 大写词（空白分隔） |
| Quote | 引号 |
| Bracket | 方括号 |
| Parenthesis | 圆括号 |
| Brace | 花括号 |
| Angle Bracket | 尖括号 |
| Backquote | 反引号 |
| Delimiter | 分隔符 |
| Range | 范围 |
| Grapheme | 图素 |
| Segment | 分割 |
| Nesting | 嵌套 |
