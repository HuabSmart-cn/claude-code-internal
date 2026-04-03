# native-ts

## 功能
纯 TypeScript 实现的原生模块替代品。用于替代原本依赖 Rust/C++ NAPI 原生模块的功能，实现在不依赖原生编译的情况下提供相同功能。

**注意**: 此目录没有 `.ts` 文件，主要包含纯 TypeScript 实现的子模块。

## 子目录

### native-ts/color-diff/
**语法高亮差异对比模块**

纯 TypeScript 端口，替代 `vendor/color-diff-src`（Rust 版本使用 syntect+bat）。

- 使用 `highlight.js` 进行语法高亮（替代 Rust 的 syntect）
- 使用 `diff` npm 包的 `diffArrays` 进行单词对比
- API 与 `vendor/color-diff-src/index.d.ts` 完全匹配

**主要类型**:
- `Hunk` - 差异块
- `SyntaxTheme` - 语法主题
- `NativeModule` - 原生模块接口

**限制**: 由于 hljs 语法覆盖差异，部分 token（如 `=` `:` 等）可能不在高亮范围内。

### native-ts/file-index/
**高性能模糊文件搜索模块**

纯 TypeScript 端口，替代 `vendor/file-index-src`（Rust NAPI 模块，基于 nucleo）。

- `FileIndex` 类 - 模糊搜索索引
- `loadFromFileList(fileList: string[])` - 加载路径列表并建立索引
- `search(query: string, limit: number)` - 执行模糊搜索
- 异步版本 `loadFromFileListAsync()` 支持大文件列表（27万+文件）分块处理

**评分语义**: 分数越低越好（0.0 为最佳匹配）
- 路径含 "test" 的文件会有 1.05× 惩罚

**性能优化**:
- 基于时间的分块策略，避免主线程阻塞
- 顶层结果缓存（TOP_LEVEL_CACHE_LIMIT = 100）
- 支持在索引构建过程中执行查询

### native-ts/yoga-layout/
**Flexbox 布局引擎**

纯 TypeScript 端口，替代 Meta 的 yoga-layout（C++ 实现）。

**实现的特性**（Ink 实际使用的子集）:
- flex-direction (row/column + reverse)
- flex-grow / flex-shrink / flex-basis
- align-items / align-self
- justify-content
- margin / padding / border / gap
- width / height / min / max
- position: relative / absolute
- display: flex / none
- measure functions (文本节点)

**额外实现**（规范兼容性）:
- margin: auto
- flex-wrap / wrap-reverse
- align-content
- display: contents
- baseline alignment

**未实现**（Ink 不使用）:
- aspect-ratio
- box-sizing: content-box
- RTL direction

**导出的枚举**:
`Align`, `BoxSizing`, `Dimension`, `Direction`, `Display`, `Edge`, `Errata`, `ExperimentalFeature`, `FlexDirection`, `Gutter`, `Justify`, `MeasureMode`, `Overflow`, `PositionType`, `Unit`, `Wrap`

## 架构说明

这些纯 TypeScript 端口是为了消除对原生 NAPI 模块的依赖，使代码可以在更多环境（如 WebAssembly、纯 JS 环境）中运行。每个端口都尽量匹配原生 API 的接口签名，以便于无缝替换。
