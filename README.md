# 🌧️ 及时雨书签可视化 · Bookmark Visualizer Skill

一个 Claude Agent Skill，将 Chrome 书签导出文件转化为复古终端风格的可视化导航网页。

![风格预览](https://img.shields.io/badge/风格-复古终端-7aff4a?style=flat-square&labelColor=0d0f0a)
![书签支持](https://img.shields.io/badge/支持-Chrome%20书签-4affec?style=flat-square&labelColor=0d0f0a)
![单文件输出](https://img.shields.io/badge/输出-单HTML文件-ffb830?style=flat-square&labelColor=0d0f0a)

---

## ✨ 效果特色

- **CRT 复古终端风格** — 扫描线、磷光绿发光效果，致敬 [ccunpacked.dev](https://ccunpacked.dev)
- **智能分类** — 自动按 AI工具、编程、学习、效率工具等分类归档
- **实时搜索** — 输入即过滤，无需刷新
- **侧边栏导航** — 分类列表 + 数量角标，一键切换视图
- **完全独立** — 输出单个 HTML 文件，浏览器直接打开，无需服务器

---

## 🚀 安装使用

### 方法一：通过 Claude.ai Skills 安装

1. 下载 [`SKILL.md`](./SKILL.md)
2. 在 Claude.ai → Settings → Skills 中上传
3. 上传 Chrome 书签文件，告诉 Claude：**"帮我把书签做成可视化网页"**

### 方法二：通过 Claude Code 使用

```bash
# 克隆此仓库
git clone https://github.com/YOUR_USERNAME/bookmark-visualizer-skill.git

# 将 SKILL.md 添加到你的 Claude Code skills 目录
cp bookmark-visualizer-skill/SKILL.md ~/.claude/skills/bookmark-visualizer/SKILL.md
```

---

## 📖 如何导出 Chrome 书签

1. Chrome 右上角 `⋮` → **书签和列表 → 书签管理器**
2. 书签管理器右上角 `⋮` → **导出书签**
3. 保存为 `.html` 文件
4. 上传给 Claude，告诉它目标文件夹名（如"及时雨"）

---

## 🗂️ 支持的分类

| 图标 | 分类 | 覆盖内容 |
|------|------|---------|
| 🤖 | AI 对话助手 | Claude, Gemini, DeepSeek, Grok 等 |
| 💻 | AI 编程工具 | Cursor, Cline, Claude Code, Lovable 等 |
| 🕸️ | AI Agent & 工作流 | Manus, n8n, AutoGen, OpenClaw 等 |
| 🧠 | Agent Skills | Skills 市场, MCP, 提示词工程 |
| ⚡ | AI 平台 & API | HuggingFace, OpenRouter, ElevenLabs 等 |
| 📚 | LLM 学习资源 | 论文, 课程, Lil'Log, MiniMind 等 |
| 🧮 | 算法 & 数据结构 | LeetCode, Hello算法, labuladong |
| 🛠️ | 效率工具 | Excalidraw, Zread, TLDW, Podwise 等 |
| 🎨 | 设计 & 创作 | Figma, Dribbble, 小红书生成器等 |
| 🎯 | 个人成长 | N-Back 训练, Paul Graham, 打字练习 |
| 🎓 | 简历 & 职业 | 魔方简历, 面试, 作品集灵感 |
| 📦 | 其他 | 未分类书签 |

> 分类规则完全可自定义，在 `SKILL.md` 的分类表格中修改即可

---

## 🔄 更新书签

当你的书签有更新时，重新导出 Chrome 书签文件，上传给 Claude：

> "我更新了书签，帮我重新生成可视化网页"

Claude 会自动对比差异，保留原有分类方案，输出带时间戳的新版文件。

---

## 📁 文件结构

```
bookmark-visualizer-skill/
├── SKILL.md              # Claude Skill 指令文件（核心）
├── README.md             # 本文件
└── examples/
    └── demo.html         # 示例输出（可在浏览器直接预览）
```

---

## 🛠️ 技术栈

- **纯 HTML/CSS/JS** — 零依赖，单文件输出
- **Google Fonts** — VT323 + Share Tech Mono + Courier Prime
- **CSS 动画** — CRT 扫描线、发光效果、卡片渐入
- **Vanilla JS** — 实时搜索、分类过滤、路由

---

## 📄 License

MIT — 随便用，欢迎 PR 改进分类规则或设计风格

---

*由 Claude 生成 · Powered by Anthropic Agent Skills*
