# AI 小白入门分享 - 赛博朋克幻灯片

> 手机端一屏一章 / 卡片式滑动体验 · 赛博朋克风格 · 像素趣味插画

---

## 项目路径

```
ai-beginner-deck/
├── index.html    ← 全部代码（HTML + CSS + JS，单文件）
├── README.md     ← 本文件
└── SPEC.md       ← 设计规格说明
```

---

## 如何运行

### 本地预览（任选一种）

```bash
# 方式1：直接用浏览器打开
open index.html

# 方式2：Python 静态服务器（支持手机扫码预览）
cd ai-beginner-deck
python3 -m http.server 8080
# 然后手机/浏览器访问 http://你的IP:8080

# 方式3：Node serve
npx serve .
```

> 手机和电脑在同一 WiFi 下时，用 `ifconfig` 查本机 IP，手机访问 `http://<电脑IP>:8080`

---

## 技术栈

| 层次 | 技术 |
|------|------|
| 结构 | 语义化 HTML5 |
| 样式 | 内联 CSS（CSS Variables + Flexbox + Grid） |
| 交互 | 原生 JavaScript（Touch / Wheel / Keyboard） |
| 图标/插画 | 内联 SVG + CSS pixel art（零外部依赖） |
| 字体 | 系统字体栈（避免外部字体加载） |

**无框架 · 无构建工具 · 无外部依赖 · 单文件即可运行**

---

## 章节信息架构（11 屏）

| # | 章节 | 类型 |
|---|------|------|
| 0 | Hero / 封面 | 全屏欢迎页 |
| 1 | 为什么每个人都该懂 AI | 内容页 |
| 2 | 名词概念卡组（13张概念卡） | 卡片组 |
| 3 | 大模型为什么看起来聪明 | 内容页 |
| 4 | Agent 是什么 | 内容页 |
| 5 | Agent 为什么火 | 内容页 |
| 6 | Agent 应用场景 | 场景卡 |
| 7 | 企业踩坑 | 内容页 |
| 8 | AI 热点 | 内容页 |
| 9 | 入门建议 | 内容页 |
| 10 | 总结页 | 全屏结束页 |

---

## 设计取舍

### 做了
- **手机优先**：所有布局基于 375px 宽度设计，大屏时居中加边距
- **触滑翻页**：基于 `touchstart/touchend` 计算滑动方向，阈值 50px
- **滚轮翻页**：`wheel` 事件，节流 800ms 防止刷屏
- **键盘翻页**：← → 方向键 / PageUp / PageDown
- **进度指示**：底部圆点 + 数字显示当前进度
- **章节跳转**：点击进度指示器可直接跳转
- **像素插画**：全部用 CSS/SVG 内联生成，不依赖外部资源
- **概念卡组**：横向滑动，每卡一个概念，带 emoji/icon
- **Cyberpunk 配色**：深色背景 + 霓虹色（青/品红/黄/绿）

### 没做（首版范围）
- 不做懒加载/预加载优化（内容量级不需要）
- 不做 PWA / Service Worker
- 不做深色/浅色模式切换
- 不做多语言
- 不做内容搜索
- 概念卡横向滑动无独立进度条（依赖主进度指示器）

---

## 自定义内容

内容直接写在 `index.html` 的 `<script>` 区块里，以章节数组组织：

```javascript
const chapters = [
  { id, title, subtitle, content, type, pixelArt },
  // ...
];
```

修改内容只需编辑这个数组，无需碰 CSS/JS 逻辑。

---

## 浏览器兼容

- iOS Safari 14+
- Android Chrome 90+
- 现代桌面浏览器（Chrome / Firefox / Safari / Edge）

不支持 IE。
