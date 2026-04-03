# ink/layout

## 功能
基于 Yoga 引擎的布局系统，处理 flexbox 布局计算。

## 文件说明

| 文件 | 功能 |
|------|------|
| `engine.ts` | Yoga 布局引擎封装 |
| `geometry.ts` | 几何计算工具 |
| `node.ts` | 布局节点抽象 |
| `yoga.ts` | Yoga 绑定 |

## 核心概念

### Yoga 布局引擎
Facebook 开源的 flexbox 实现，提供了高性能的跨平台布局计算。

### 布局节点 (Node)
对应 DOM 中的元素概念：
- 尺寸属性 (width, height)
- 边距 (margin)
- 内边距 (padding)
- 边框 (border)
- 位置 (position)

### 布局计算流程
1. 创建布局节点
2. 设置节点属性
3. 添加子节点
4. 计算布局 (YGNodeCalculateLayout)
5. 获取结果 (getComputedLayout)

### 单位
- 固定值：像素
- 百分比：相对于父容器
- AUTO：自动计算
- GAP：间距
