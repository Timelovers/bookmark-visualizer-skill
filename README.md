<div align="center">

# 🌧️ 及时雨书签可视化 · Bookmark Visualizer Skill
### *Your Chrome bookmarks, rerouted through a CRT—one HTML file, zero backend.*
### *导出书签 → 磷光绿终端里重新排版，单文件带走。*

![风格预览](https://img.shields.io/badge/风格-复古终端-7aff4a?style=flat-square&labelColor=0d0f0a)
![书签支持](https://img.shields.io/badge/支持-Chrome%20书签-4affec?style=flat-square&labelColor=0d0f0a)
![单文件输出](https://img.shields.io/badge/输出-单HTML文件-ffb830?style=flat-square&labelColor=0d0f0a)

</div>

---

<div align="center">

**[English](#english) · [中文](#chinese)**

</div>

---

<a name="english"></a>

## What is this?

A **Claude Agent Skill** that ingests Chrome’s exported `bookmarks_*.html`, auto-clusters links by domain/title heuristics, and emits a **single self-contained HTML** you can double-click—CRT aesthetics borrowed from the [ccunpacked.dev](https://ccunpacked.dev) vibe, not from a component library.

No build step. No npm install on the output. If it opens in a browser, it works.

## ✨ Features

- 🖥️ **CRT terminal skin** — scanlines, phosphor green glow, amber accents—readable nostalgia, not toy pixels
- 🧭 **Smart buckets** — AI tools, coding, learning, productivity—rules live in `SKILL.md`, tweak if your stack drifts
- 🔎 **Live search** — filters cards as you type; no round-trip, no “search page”
- 📌 **Sidebar + counts** — jump categories, see how fat each folder got
- 📄 **One file out** — inline CSS/JS/fonts hook; air-gap friendly

## 🎬 Motion (regenerated)

Static HTML doesn’t mean dead UI. The template bakes in:

- **Scanline overlay** — low-opacity repeating gradient so the panel feels like glass, not a flat PNG
- **Phosphor bloom** — `text-shadow` / `box-shadow` tuned so links glow on hover without washing out body copy
- **Staggered entrance** — cards use short translate + opacity keyframes so the grid doesn’t pop in as one ugly rectangle
- **Caret blink** — header/meta accents use a tight `blink` cycle for terminal credibility

All motion is CSS-only—no framework, no runtime dependency.

## 🛠️ Tech Stack

```
Output:      Single HTML (inline CSS + JS)
Fonts:       VT323 · Share Tech Mono · Courier Prime (Google Fonts)
Runtime:     Vanilla JS — filter, counts, sidebar routing
Skill host:  Claude Skills / Claude Code — SKILL.md drives extraction + codegen
```

## 🚀 Install & Use

**Option A — Claude (hosted)**

1. Download [`SKILL.md`](./SKILL.md)
2. Claude → Settings → Skills → upload
3. Export Chrome bookmarks → upload → say: *Turn this into the terminal bookmark page*

**Option B — Claude Code**

```bash
git clone https://github.com/Timelovers/bookmark-visualizer-skill.git
mkdir -p ~/.claude/skills/bookmark-visualizer
cp bookmark-visualizer-skill/SKILL.md ~/.claude/skills/bookmark-visualizer/SKILL.md
```

Typical triggers:

```
Bookmark export is in uploads — build the CRT gallery for folder 「及时雨」
可视化我的 Chrome 书签，复古终端风格，单文件输出
```

## 📖 Export bookmarks (Chrome)

1. Chrome menu → **Bookmarks → Bookmark Manager**
2. Organize → **Export bookmarks** → save `bookmarks_*.html`
3. Pass the file (and optional folder name like「及时雨」) to the agent running this skill

## 🗂️ Preview

Open [`examples/demo.html`](./examples/demo.html) locally to see the output shape—swap in your data via the skill workflow.

## 📬 Contact

- GitHub: [@Timelovers](https://github.com/Timelovers)
- Website: [lijiaxing.com.cn](https://lijiaxing.com.cn/)

---

<a name="chinese"></a>

## 这是什么？

面向 Claude 的 **Agent Skill**：读取 Chrome 导出的 **`bookmarks_*.html`**，按域名与标题关键词做**智能归类**，生成可在浏览器直接打开的**复古终端风单页 HTML**（审美致敬 [ccunpacked.dev](https://ccunpacked.dev)）。

生成物零依赖、无构建：只要浏览器能开本地文件，就能用。

## ✨ 效果特色

- 🖥️ **CRT 复古终端** — 扫描线、磷光绿层次光，阅读优先，不是廉价像素滤镜
- 🧭 **智能分类** — AI 工具、编程、学习、效率等归档规则写在 `SKILL.md`，可按你的书签生态改表
- 🔎 **实时搜索** — 输入即过滤，无需刷新整页
- 📌 **侧边栏导航** — 分类列表 + 数量角标，一键切换视图
- 📄 **完全独立** — 输出单个 HTML，离线双击可用，无需服务器

## 🎬 动效（新版说明）

单文件不代表静态死板。模板内置：

- **扫描线叠层** — 低透明度 repeating gradient，屏幕像玻璃面板而非一张扁图
- **磷光发光** — hover 时链接绿色亮边与阴影层级可控，正文不被眩光淹没
- **卡片错峰入场** — 短位移 + 透明度关键帧，避免整块网格「啪」一下出现
- **光标闪烁** — 头部信息条用紧凑 `blink` 周期，终端气质到位

动效全部为 **纯 CSS**，无框架、无额外运行时。

## 🛠️ 技术栈

```
产物：      单 HTML（内联样式与脚本）
字体：      VT323 · Share Tech Mono · Courier Prime（Google Fonts）
交互：      原生 JS — 搜索、计数、侧栏切换
Skill：     SKILL.md 定义解析书签与生成模板流程
```

## 🚀 安装使用

**方式一：Claude 网页版 Skills**

1. 下载 [`SKILL.md`](./SKILL.md)
2. Claude → Settings → Skills → 上传
3. 导出书签并上传，说明：**「帮我把书签做成复古终端可视化网页」**

**方式二：Claude Code**

```bash
git clone https://github.com/Timelovers/bookmark-visualizer-skill.git
mkdir -p ~/.claude/skills/bookmark-visualizer
cp bookmark-visualizer-skill/SKILL.md ~/.claude/skills/bookmark-visualizer/SKILL.md
```

常用触发：

```
书签 html 已上传 —— 对「及时雨」文件夹生成 CRT 导航页
Chrome 书签导出好了，单文件、要能离线打开
```

## 📖 导出 Chrome 书签

1. Chrome 右上角 `⋮` → **书签和列表 → 书签管理器**
2. 管理器右上角 `⋮` → **导出书签**，保存为 `.html`
3. 交给运行本 Skill 的 Agent，可指定文件夹名（如「及时雨」）

## 🗂️ 示例

本地打开 [`examples/demo.html`](./examples/demo.html) 可预览页面骨架；真实数据由 Skill 根据你的导出文件生成。

## 📬 联系方式

- GitHub：[@Timelovers](https://github.com/Timelovers)
- 主页：[lijiaxing.com.cn](https://lijiaxing.com.cn/)

---

> 「书签如雨，终端接得住。」
>
> *Bookmarks fall like rain—the terminal catches what matters.*

---

<div align="center">

**License:** MIT · 分类规则与样式欢迎 PR

Made with 💜 by [Sara](https://lijiaxing.com.cn/) · [@Timelovers](https://github.com/Timelovers)

</div>
