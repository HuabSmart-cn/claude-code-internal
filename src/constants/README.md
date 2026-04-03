# constants

## 功能
常量定义模块，包含应用级常量、API 限制、配置常量等。

## 文件说明

- `apiLimits.ts` - API 限制常量
- `betas.ts` - Beta 功能标志
- `common.ts` - 通用常量
- `cyberRiskInstruction.ts` - 网络风险指令
- `errorIds.ts` - 错误 ID
- `figures.ts` - 图形字符 (Unicode 符号)
- `files.ts` - 文件相关常量
- `github-app.ts` - GitHub App 配置
- `keys.ts` - 键名常量
- `messages.ts` - 消息常量
- `oauth.ts` - OAuth 配置
- `outputStyles.ts` - 输出样式常量
- `product.ts` - 产品常量
- `prompts.ts` - 提示词常量
- `spinnerVerbs.ts` - 加载动画动词
- `system.ts` - 系统常量
- `systemPromptSections.ts` - 系统提示部分
- `toolLimits.ts` - 工具限制
- `tools.ts` - 工具常量
- `turnCompletionVerbs.ts` - 回合完成动词
- `xml.ts` - XML 常量

## 主要常量分类

### API 与限制
- `apiLimits.ts` - API 调用频率和配额限制
- `toolLimits.ts` - 工具使用限制

### 认证与 OAuth
- `oauth.ts` - OAuth 2.0 配置
- `github-app.ts` - GitHub App 配置

### UI 与输出
- `figures.ts` - Unicode 图形 (如 ✓, ✗, →)
- `outputStyles.ts` - 终端输出样式
- `spinnerVerbs.ts` - 加载动画的动词 (loading, working...)
- `turnCompletionVerbs.ts` - 对话完成提示词

### 系统配置
- `system.ts` - 系统级常量
- `systemPromptSections.ts` - 系统提示结构
- `prompts.ts` - 预定义提示词模板

### Beta 功能
- `betas.ts` - 实验性功能开关

### 错误处理
- `errorIds.ts` - 错误类型标识
- `cyberRiskInstruction.ts` - 安全风险提示
