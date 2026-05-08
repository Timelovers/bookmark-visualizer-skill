<div align="center">

# 🌧️ 及时雨书签可视化 · Bookmark Visualizer Skill
### *Your Chrome bookmarks, rerouted through a CRT—one HTML file, zero backend.*
### *导出书签 → 磷光绿终端里重新排版，单文件带走。*

![风格预览](https://img.shields.io/badge/风格-复古终端-7aff4a?style=flat-square&labelColor=0d0f0a)
![书签支持](https://img.shields.io/badge/支持-Chrome%20书签-4affec?style=flat-square&labelColor=0d0f0a)
![单文件输出](https://img.shields.io/badge/输出-单HTML文件-ffb830?style=flat-square&labelColor=0d0f0a)

<br />

</div>

---

<div align="center">

**[English](#english) · [中文](#chinese)**

</div>

---

<a name="english"></a>

## What is this?

A **Claude Agent Skill** that reads Chrome’s `bookmarks_*.html`, buckets links with domain/title heuristics, and writes **one self-contained HTML** you can open offline—CRT look inspired by [ccunpacked.dev](https://ccunpacked.dev), implemented as plain CSS/JS, not a UI kit.

No bundler on the artifact: if your browser opens local files, you’re done.

## 🎯 When to use it

- You exported Chrome bookmarks and want a **navigable gallery**, not a folder dump
- You care about **retro terminal aesthetics** + search, without hosting anything
- You’re fine letting Claude **parse HTML + emit HTML** (the skill encodes the pipeline)

## 📥 Input → 📤 Output

| | |
|---|---|
| **In** | Chrome bookmark export (`bookmarks_*.html`), optional folder name (e.g.「及时雨」) to scope a subtree |
| **Out** | Single `.html` — sidebar categories, counts, live filter, bookmark cards; fonts pulled from Google Fonts |

Minimal prompt example:

```
Here’s my bookmarks export. Build the CRT-style single-file page; focus folder 「及时雨」.
```

## ✨ Features

- 🖥️ **CRT terminal skin** — scanlines, phosphor green, amber accents; readable, not gimmicky
- 🧭 **Smart buckets** — AI / coding / learning / tools… rules live in `SKILL.md` for edits
- 🔎 **Live search** — filters as you type
- 📌 **Sidebar + counts** — jump categories, see weight per bucket
- 📄 **One artifact** — inline CSS/JS; air-gap friendly

## 🎬 Motion

CSS-only: scanline overlay, phosphor hover glow, staggered card entrance, blink accents—no extra runtime.

## 🛠️ Tech Stack

```
Ship unit:   Single HTML (inline CSS + JS)
Fonts:       VT323 · Share Tech Mono · Courier Prime (Google Fonts)
Runtime:     Vanilla JS — search, counts, sidebar
Host:        Claude Skills / Claude Code — SKILL.md owns parse + codegen
```

## 🚀 Quick Start

**Claude (hosted)**

1. Grab [`SKILL.md`](./SKILL.md) → Settings → Skills → upload  
2. Export bookmarks → attach file → ask for the terminal page  

**Claude Code**

```bash
git clone https://github.com/Timelovers/bookmark-visualizer-skill.git
mkdir -p ~/.claude/skills/bookmark-visualizer
cp bookmark-visualizer-skill/SKILL.md ~/.claude/skills/bookmark-visualizer/SKILL.md
```

**Cursor Agent Skills**（可选）

```bash
mkdir -p ~/.cursor/skills/bookmark-visualizer
cp SKILL.md ~/.cursor/skills/bookmark-visualizer/SKILL.md
```

Trigger ideas:

```
Bookmark export is in uploads — CRT gallery for folder 「及时雨」
可视化 Chrome 书签，复古终端，单文件输出
```

## 📖 Export bookmarks (Chrome)

1. Chrome → **Bookmarks → Bookmark Manager**  
2. **Export bookmarks** → save `bookmarks_*.html`  
3. Hand the file + optional folder label to the agent running this skill  

## 🗂️ Preview

[`examples/demo.html`](./examples/demo.html) shows the shell; real data comes from your export via the skill.

## 📬 Contact

- GitHub: [@Timelovers](https://github.com/Timelovers)  
- Website: [lijiaxing.com.cn](https://lijiaxing.com.cn/)

---

<a name="chinese"></a>

## 这是什么？

给 Claude 用的 **Agent Skill**：读入 Chrome 的 **`bookmarks_*.html`**，按域名/标题关键词归类，输出**一个可离线打开的复古终端风 HTML**（审美参考 [ccunpacked.dev](https://ccunpacked.dev)）。产物无构建、无 npm，浏览器能开本地文件就能用。

## 🎯 什么时候用

- 书签导出一大堆，想要**能搜、能分类看的导航页**，而不是文件夹里乱堆  
- 想要 **CRT 终端质感 + 实时过滤**，又不想部署服务器  
- 接受由 Claude **解析书签 HTML 再生成展示 HTML**（流程写在 `SKILL.md`）

## 📥 输入与输出

| | |
|---|---|
| **输入** | Chrome 导出文件（`bookmarks_*.html`）；可选指定书签栏子文件夹名（如「及时雨」）只渲染该枝 |
| **输出** | 单个 `.html`：侧栏分类与数量角标、搜索框、书签卡片栅格；字体走 Google Fonts |

一句话示例：

```
这是我的书签导出，请生成复古终端单文件页面，只看「及时雨」文件夹。
```

## ✨ 功能亮点

- 🖥️ **CRT 复古终端** — 扫描线、磷光绿、琥珀点缀；耐看，不是廉价像素堆叠  
- 🧭 **智能分类** — AI 工具、编程、学习、效率等；规则表在 `SKILL.md` 可改  
- 🔎 **实时搜索** — 输入即过滤  
- 📌 **侧边栏 + 角标** — 分类跳转，数量一目了然  
- 📄 **单文件产物** — 内联样式脚本，离线双击可用  

## 🎬 动效

纯 CSS：扫描线叠层、链接 hover 磷光、卡片错峰入场、标题区 blink——无额外框架。

## 🛠️ 技术栈

```
交付物：    单 HTML（内联 CSS / JS）
字体：      VT323 · Share Tech Mono · Courier Prime
交互：      原生 JS
Skill：     SKILL.md 负责解析与模板生成
```

## 🚀 快速开始

**Claude 网页版 Skills**

1. 下载 [`SKILL.md`](./SKILL.md) → Skills 里上传  
2. 导出书签 → 上传附件 → 说明要做终端风页面  

**Claude Code**

```bash
git clone https://github.com/Timelovers/bookmark-visualizer-skill.git
mkdir -p ~/.claude/skills/bookmark-visualizer
cp bookmark-visualizer-skill/SKILL.md ~/.claude/skills/bookmark-visualizer/SKILL.md
```

**Cursor 技能目录（可选）**

```bash
mkdir -p ~/.cursor/skills/bookmark-visualizer
cp SKILL.md ~/.cursor/skills/bookmark-visualizer/SKILL.md
```

常用触发：

```
书签 html 已上传 —— 给「及时雨」生成 CRT 导航页
Chrome 书签导出好了，单文件、离线可开
```

## 📖 导出 Chrome 书签

1. Chrome `⋮` → **书签和列表 → 书签管理器**  
2. `⋮` → **导出书签** → 保存为 `.html`  
3. 把文件（及可选文件夹名）交给运行本 Skill 的 Agent  

## 🗂️ 示例预览

本地打开 [`examples/demo.html`](./examples/demo.html) 看页面骨架；真实书签数据由 Skill 按你的导出生成。

## 📬 联系方式

- GitHub：[@Timelovers](https://github.com/Timelovers)  
- 主页：[lijiaxing.com.cn](https://lijiaxing.com.cn/)

---

> 「书签如雨，终端接得住。」
>
> *Bookmarks fall like rain—the terminal catches what matters.*

---

<div align="center">

**License:** MIT · 欢迎 PR 改进分类与样式

Made with 💜 by [Sara](https://lijiaxing.com.cn/) · [@Timelovers](https://github.com/Timelovers)

</div>
