# ink/termio

## 功能
终端 IO 处理模块，负责解析和生成 ANSI/VT100 转义序列。

## 文件说明

| 文件 | 功能 |
|------|------|
| `ansi.ts` | ANSI 基本序列 |
| `csi.ts` | CSI (Control Sequence Introducer) 序列 |
| `dec.ts` | DEC 私有序列 |
| `esc.ts` | ESC 转义序列 |
| `osc.ts` | OSC (Operating System Command) 序列 |
| `parser.ts` | 序列解析器 |
| `sgr.ts` | SGR (Select Graphic Rendition) 序列 |
| `tokenize.ts` | 标记化/分词 |
| `types.ts` | 类型定义 |

## 核心概念

### ANSI 转义序列
终端控制语言，以 ESC (`\x1b` 或 `\033`) 开头。

### CSI 序列
格式：`ESC [ 参数 ; ... 命令`
- 光标移动：`ESC [ row ; col H`
- 清屏：`ESC [ 2 J`
- 设置样式：`ESC [ 1 m` (粗体)

### SGR 序列
用于设置文本属性：
- 颜色 (0-255 或 RGB)
- 粗体、斜体、下划线
- 背景色

### OSC 序列
操作系统命令：
- 设置窗口标题：`ESC ] 2 ; title BEL`
- 链接：`ESC ] 8 ; params ; URI BEL`

### 解析器
将终端输入的字节流解析为事件（按键、鼠标、颜色码等）。

### 分词器
将字符串分割为文本片段和转义序列。
