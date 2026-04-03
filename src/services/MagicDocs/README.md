# services/MagicDocs - 文档生成

## 功能

MagicDocs 自动为代码生成文档，解释代码功能和用法。

## 文件列表

| 文件 | 功能 |
|------|------|
| `magicDocs.ts` | 文档生成核心 |
| `prompts.ts` | 文档生成提示词 |

## 生成类型

### 1. 函数文档
```typescript
/**
 * 计算两个数的和
 * @param a 第一个数
 * @param b 第二个数
 * @returns 两个数的和
 */
function add(a: number, b: number): number
```

### 2. 文件概述
```typescript
/**
 * 用户认证模块
 * 负责处理用户登录、注册和密码重置
 * 依赖: bcrypt, jsonwebtoken
 */
```

### 3. API 文档
```typescript
/**
 * POST /api/users
 * 创建新用户
 * Body: { name: string, email: string }
 * Returns: { id: string, name: string, email: string }
 */
```

## 生成流程

```
源代码
    ↓
prompts.ts 分析
    ↓
AI 生成文档
    ↓
格式化输出 (Markdown/JSdoc/OpenAPI)
```

## 输出格式

| 格式 | 适用场景 |
|------|----------|
| JSDoc | TypeScript/JavaScript |
| Markdown | README 文件 |
| OpenAPI | API 端点 |
| reStructuredText | Python |
