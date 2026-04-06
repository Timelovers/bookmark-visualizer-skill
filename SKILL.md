---
name: bookmark-visualizer
description: >
  将 Chrome 书签 HTML 导出文件转化为复古终端风格的可视化网页（参考 ccunpacked.dev 的美学风格）。
  触发场景：用户上传 Chrome 书签文件（bookmarks_*.html）、提到"书签可视化"、"书签网页"、"书签导航页"、
  "把书签做成网页"、"书签整理"，或者任何希望将浏览器书签转为漂亮展示页面的请求时，必须使用此技能。
  即使用户只是说"帮我整理书签"或"书签太乱了"，也应主动建议并使用此技能。
  输出：一个独立的 HTML 文件，包含：CRT 复古终端风格设计、智能分类侧边栏、实时搜索、
  按分类分组展示所有书签卡片，可直接在浏览器中打开使用。
---

# 书签可视化技能 · Bookmark Visualizer

将 Chrome 导出的书签 HTML 转化为复古终端风格的可视化导航网页。

## 工作流程

### 第一步：读取书签文件

用户上传的 bookmarks_*.html 文件位于 `/mnt/user-data/uploads/`，使用 bash 提取特定文件夹内容：

```python
import re

with open('/mnt/user-data/uploads/<文件名>.html', 'r', encoding='utf-8') as f:
    content = f.read()

# 定位目标文件夹（如"及时雨"）
folder_name = '目标文件夹名'
start = content.find(folder_name)
dl_start = content.find('<DL>', start)

# 用深度计数提取完整 DL 块
depth = 0
i = dl_start
while i < len(content):
    if content[i:i+4] == '<DL>':
        depth += 1; i += 4
    elif content[i:i+5] == '</DL>':
        depth -= 1
        if depth == 0: dl_end = i + 5; break
        i += 5
    else:
        i += 1

section = content[dl_start:dl_end]

# 提取所有链接
links = re.findall(r'<A HREF="([^"]+)"[^>]*>([^<]+)</A>', section)
# 返回 [(url, title), ...]
```

若用户未指定文件夹，提取书签栏全部内容；若文件夹嵌套，递归处理。

### 第二步：智能分类

根据链接的域名、标题关键词，将书签归类到以下参考分类（可根据实际内容灵活调整）：

| 分类 ID | 图标 | 参考分类名 | 关键词示例 |
|---------|------|-----------|-----------|
| ai-chat | 🤖 | AI 对话助手 | claude, grok, gemini, deepseek, kimi, 豆包, perplexity, copilot |
| ai-code | 💻 | AI 编程工具 | cursor, cline, kilo, lovable, flowith, repomix, aider, opencode |
| ai-agent | 🕸️ | AI Agent & 工作流 | manus, n8n, autogen, openclaw, lobster, coze |
| ai-skills | 🧠 | Agent Skills | skills.sh, skillsmp, mcp, prompt, snackprompt |
| ai-platform | ⚡ | AI 平台 & API | huggingface, openrouter, elevenlabs, api_keys, platform |
| llm-learn | 📚 | LLM 学习资源 | arxiv, github+llm, datawhale, minimind, lil'log |
| algo-ds | 🧮 | 算法 & 数据结构 | leetcode, neetcode, grind75, labuladong, hello-algo |
| tools | 🛠️ | 效率工具 | excalidraw, figma, tldw, zread, sojson, boardmix |
| design | 🎨 | 设计 & 创作 | dribbble, midjourney, aura, saaspo, 小红书, pixmiller |
| learning | 🎯 | 个人成长 | paulgraham, dual-n-back, typing, youtube, reddit |
| career | 🎓 | 简历 & 职业 | resume, cv, portfolio, interview, leetcode |
| misc | 📦 | 其他 | 不属于以上任何分类的书签 |

**分类原则：**
- 优先按域名判断（github.com/anthropics → AI 相关）
- 其次按标题关键词
- 书签数量 < 5 的分类可合并到 misc
- 总书签数 > 200 时，可细分子类

### 第三步：生成 HTML

参考以下模板结构生成**单文件 HTML**（内联所有 CSS/JS）：

#### 设计规范（复古终端风格）

```
色彩系统（必须使用 CSS 变量）：
--bg: #0d0f0a          深黑绿背景
--green: #7aff4a       主色调磷光绿
--amber: #ffb830       强调色琥珀黄
--cyan: #4affec        链接色青色
--text: #c8d4a0        正文色
--text-dim: #6a7a50    次要文字
--border: #2a2e1a      边框色

字体（按优先级）：
1. 'VT323' - 复古像素字体，用于大标题/Logo
2. 'Share Tech Mono' - 终端等宽字体，用于 UI 元素
3. 'Courier Prime' - 优雅等宽字体，用于正文
从 Google Fonts 加载：https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Courier+Prime:wght@400;700&family=VT323&display=swap

必选视觉效果：
- CRT 扫描线（repeating-linear-gradient 叠加层）
- 磷光发光效果（text-shadow + box-shadow）
- 光标闪烁动画（blink keyframe）
- 卡片 hover 时绿色边框发光
- 页面加载时卡片渐入动画（fadeup）

布局：
- 顶部 Header：Logo + 统计信息 + 标签导航栏
- 左侧 Sidebar（220px）：分类列表 + 数量角标，sticky 固定
- 右侧 Main：搜索框 + 书签卡片网格（auto-fill, minmax(280px, 1fr)）
- 底部 Footer：版权信息
```

#### JS 数据结构

```javascript
const DATA = {
  categories: [
    {
      id: 'cat-id',        // 唯一标识
      icon: '🤖',          // emoji 图标
      name: '分类名称',     // 显示名
      desc: 'English desc', // 英文副标题
      items: [
        { title: '书签标题', url: 'https://...' },
        // ...
      ]
    },
    // ...
  ]
};
```

#### 核心功能（必须实现）

1. **实时搜索**：输入框过滤标题 + 域名，无需刷新
2. **侧边栏分类切换**：点击切换当前视图，active 状态高亮
3. **顶部标签栏**：与侧边栏联动，快速跳转
4. **ALL 分组视图**：默认按分类分组展示所有书签
5. **卡片点击**：`target="_blank"` 新标签打开链接
6. **统计状态栏**：显示当前可见数量、分类、搜索状态
7. **域名提取**：`new URL(href).hostname.replace('www.', '')`

### 第四步：输出文件

```python
# 将生成的 HTML 写入
output_path = '/mnt/user-data/outputs/bookmark-visualizer.html'
with open(output_path, 'w', encoding='utf-8') as f:
    f.write(html_content)
```

然后调用 `present_files` 工具将文件提供给用户下载。

---

## 交互细节

### 询问用户

如果书签文件包含**多个文件夹**，应先列出所有文件夹名称让用户选择：
```
发现以下书签文件夹：
- 📁 书签栏（根目录，含 XX 项）
- 📁 及时雨（XX 项）
- 📁 工作资料（XX 项）
请问要可视化哪个文件夹？还是全部？
```

### 风格询问（可选）

如用户没有指定风格，默认使用**复古终端风格**（本技能主风格）。
也可支持用户要求其他风格时，调整配色方案：
- 暗色极简：深色背景 + 白色字体
- 赛博朋克：紫色/粉色霓虹
- 纸质复古：米黄背景 + 棕色字体

### 书签数量建议

| 数量 | 建议 |
|------|------|
| < 50 | 单列大卡片，显示完整 URL |
| 50-200 | 标准 3 列卡片网格 |
| > 200 | 紧凑卡片 + 必须启用搜索和分类过滤 |
| > 500 | 建议分多个页面或启用虚拟滚动 |

---

## 更新书签工作流

当用户**重新上传新版书签文件**时：

1. 解析新文件，提取同名文件夹内容
2. 与旧版本对比：新增、删除、修改的书签
3. 重新分类（保留之前的分类方案，对新增书签归类）
4. 重新生成 HTML，保持相同的设计风格
5. 输出文件名加时间戳：`bookmark-visualizer-YYYYMMDD.html`

---

## 注意事项

- 书签 HTML 中的 `ICON` 字段含有 base64 图片数据，**不要**在网页中使用（会大幅增加文件体积），用域名首字母或 emoji 替代
- 某些 URL 可能含有 JWT token 等敏感信息（如 Medium 文章的 id_token 参数），输出时直接使用原始 URL，不做处理
- 内网 URL（如 i.zte.com.cn, 10.x.x.x）正常输出，用户自行判断是否可访问
- 书签标题过长时，卡片中用 `-webkit-line-clamp: 2` 限制为两行
- 生成的 HTML 文件应为**完全独立**的单文件，无外部依赖（Google Fonts 除外）
