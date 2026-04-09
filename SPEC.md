# SPEC - AI 小白入门分享 · 赛博朋克幻灯片

## 1. Concept & Vision

一个纯移动端消费场景的"章节卡片式"演示文稿，适合在手机微信/浏览器里滑动浏览。风格锁定赛博朋克（但不俗艳），配合内联像素画趣味插画，让 AI 入门内容不再枯燥。整体感受是：像在翻一本来自 2077 年的霓虹小人书。

## 2. Design Language

### 色彩
```
--bg:         #080818   深空背景
--bg-card:    #0d0d2b   卡片背景
--neon-cyan:  #00f5ff   霓虹青
--neon-pink:  #ff2d78   霓虹品红
--neon-yellow:#ffe600   霓虹黄
--neon-green: #39ff14   霓虹绿
--text:       #e0e0ff   主文字（淡紫白）
--text-dim:   #7070a0   辅助文字
--glow:       0 0 12px var(--neon-cyan)  发光效果
```

### 字体
- 系统字体栈：`"SF Pro Display", "PingFang SC", "Helvetica Neue", Arial, sans-serif`
- 无外部字体依赖

### 动效
- 章节切换：translateY 滑动，300ms ease-out
- 元素进入：opacity 0→1 + translateY(8px)→0，stagger 60ms
- 霓虹脉冲：CSS animation，box-shadow 呼吸效果 2s infinite
- 像素画：纯 CSS/SVG static，零动画（减少干扰）

### 图标/像素画
全部内联 SVG 或纯 CSS 生成：
- Hero：霓虹机器人像素脸
- 概念卡：每卡独立 emoji + 装饰性像素边框
- 场景卡：像素场景插画（办公室/销售/客服）
- 结语页：霓虹飞鸟

## 3. Layout & Structure

### 单屏结构（每章占一屏）
```
┌──────────────────────────┐
│  [进度条 顶部固定]         │
├──────────────────────────┤
│                          │
│     [像素插画区 约30%]     │
│                          │
├──────────────────────────┤
│                          │
│     [标题 + 副标题]        │
│                          │
├──────────────────────────┤
│                          │
│     [正文内容区]           │
│                          │
└──────────────────────────┘
│  [◀ 进度指示 ●●●●● ▶]   │  ← 底部固定导航
└──────────────────────────┘
```

### 概念卡组（横向滑动）
- 13 张卡片横向排列，snap 到每卡
- 每卡 280px 宽，高度 100% 视口
- 左右滑动切换，snap 行为

### 响应策略
- 手机优先（375px 基准）
- 桌面端 max-width: 480px 居中，两侧留黑

## 4. Features & Interactions

### 翻页
- **触滑**：touchstart/touchend 差值 > 50px 触发翻页
- **滚轮**：wheel 事件，节流 800ms
- **键盘**：← → / PageUp / PageDown / Space
- **按钮**：底部左右箭头按钮

### 进度指示
- 顶部细线进度条（实时更新）
- 底部圆点导航（点击跳转）
- 当前章节数字显示 "03/11"

### 章节切换动画
- 旧章节：translateY(0) → translateY(-30px) + opacity 0，200ms
- 新章节：translateY(30px) → translateY(0) + opacity 1，300ms

### 边界处理
- 第一页禁用向上翻页
- 最后一页禁用向下翻页
- 翻页动画期间禁止重复触发

## 5. Content

### 章节数据（11章）

**Ch0 - Hero**
- 标题：给 AI 小白的入门分享
- 副标题：从概念到 Agent · 一页读懂 AI
- 像素画：霓虹 AI 机器人像素脸

**Ch1 - 为什么每个人都该懂 AI**
- 内容：AI 渗透职场/生活/信息差/效率革命
- 像素画：像素上班族

**Ch2 - 名词概念卡组（13张）**
AI / LLM / 多模态 / Prompt / Token / Context / Fine-tuning / Inference / RAG / Hallucination / Workflow / Tools / Agent

**Ch3 - 大模型为什么看起来聪明**
- 内容：涌现能力 / Scaling Law / 压缩即智能
- 像素画：像素大脑 + 电路

**Ch4 - Agent 是什么**
- 内容：感知→规划→执行 Loop + 工具调用
- 像素画：像素机器人

**Ch5 - Agent 为什么火**
- 内容：LLM 性能触达临界点 + MCP 协议 + 成本下降
- 像素画：火焰像素图标

**Ch6 - Agent 应用场景**
- 场景卡：客服机器人 / 办公助理 / 代码助手 / 数据分析 / 销售自动化
- 像素画：各场景像素场景图

**Ch7 - 企业踩坑**
- 内容：数据安全 / Prompt 注入 / 幻觉风险 / 集成复杂度 / 成本超支
- 像素画：像素警示牌

**Ch8 - AI 热点**
- 内容：多模态 / Agent / AI Search / 本地部署 / AI 安全
- 像素画：像素热点图标

**Ch9 - 入门建议**
- 建议：先玩 ChatGPT / 搞懂 Prompt / 关注落地 / 关注安全 / 持续关注
- 像素画：像素书本

**Ch10 - 总结**
- 标题：开始你的 AI 之旅
- 副标题：了解原理 · 动手实践 · 保持好奇
- 像素画：霓虹飞鸟

## 6. Technical Approach

- 单 HTML 文件，内联 CSS + JS
- 无构建工具、无外部依赖
- CSS Variables 管理主题色
- 事件委托处理 touch/keyboard/wheel
- chapters 数组驱动渲染，数据与视图分离
