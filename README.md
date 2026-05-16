# SuperMD

Markdown 全能助手 —— 为 Claude Code 打造的 Markdown 生成、转换、审查、优化与格式切换技能。

> 由 [星核网络工作室 (SparkCore)](https://github.com/Ruyi0623) 出品

## 简介

SuperMD 是一个 Claude Code Skill，将 Markdown 文档工作流整合为五种模式，覆盖从零生成到审查优化的完整生命周期。无论是写 README、整理粘贴的笔记、检查文档格式规范、优化排版，还是在 GFM / Obsidian / MDX 之间转换，一句自然语言即可触发对应模式。

**核心特色**：

- 一技能覆盖 Markdown 全流程，无需在多个工具间切换
- 内置文档模板（README、API 文档、技术教程、学习笔记、会议记录等）
- 中文排版友好：自动处理中英文空格、标点规范
- 严格遵循文档结构原则：层级不跳跃、代码块必有语言标识、链接禁用裸 URL

## 安装

```bash
git clone https://github.com/Ruyi0623/SuperMD.git ~/.claude/skills/supermd
```

克隆后无需额外配置，Claude Code 自动加载。输入 `/supermd` 即可调用。

## 五种模式

### Generate — 从零生成

根据需求描述自动创建结构化 Markdown 文档。识别文档类型与目标受众，匹配最佳模板，输出可直接使用。

```
帮我写一份项目 API 文档
生成一篇 Next.js 入门教程
写一个本周的周报
```

支持文档类型：README、技术教程、学习笔记、API 文档、会议记录 / 周报、博客等。大型文档（>500 词）会先展示结构大纲，确认后再展开。

### Convert — 原始内容转 Markdown

将非结构化文本（HTML 片段、粘贴的笔记、松散格式内容）整理为规范 Markdown。

- 自动推断结构：发现段落分割、重复模式、表格数据
- 保留全部原始信息，去除格式噪音
- 无法判断的内容用 `<!-- Missing: ... -->` 标注，不凭空生成

### Audit — 审查诊断

逐项检查 `.md` 文件，输出三级诊断报告：

| 级别 | 内容 |
|------|------|
| 🔴 严重 | H1 不唯一、标题跳跃、裸 URL 等影响渲染的问题 |
| 🟡 建议 | 段落过长、列表风格不统一、表格对齐等可读性问题 |
| 🟢 优点 | 文档做得好的地方 |

只诊断不修改，让你全面了解问题后再决定如何处理。

### Improve — 优化改进

对现有 Markdown 文件进行结构与排版优化，直接产出优化后版本：

- 修复层级跳跃、裸 URL、无语言标签的代码块
- 统一列表符号和代码块风格
- 拆分过长段落（>7 行），合并零碎段落
- 修正中文排版（中英文空格、标点符号）
- 不改变内容含义，只改善结构与格式

### Switch — 格式转换

Markdown 风格互转：

| 源格式 | 目标格式 | 关键变更 |
|--------|----------|----------|
| GFM | Obsidian | `[text](url)` → `[[url\|text]]`，callout 转小写 |
| Obsidian | GFM | `[[wikilinks]]` → `[text](url)`，`#tags` 保留 |
| GFM | MDX | 代码块加 `live` 属性，补充 import 语句 |
| Standard | GFM | 启用自动链接、任务列表、表格、删除线 |

转换 Obsidian wikilink 时会先确认对应 `.md` 文件是否存在以正确解析路径。

## 文档结构原则

- 每个文档有且仅有一个 `# H1` 标题
- 标题层级连续，不跳跃（禁止 H1 → H3）
- 代码块始终标注语言标识，用具体语言名而非 `code`
- 链接使用描述性文字，避免裸 URL
- 图片必须有 alt 文字：`![描述文字](url)`
- 中文与英文/数字之间自动加空格，中文语境使用中文标点

## 使用示例

```bash
# 生成
/supermd 帮我写一个 VitePress 项目的产品文档

# 转换
/supermd 把这段 HTML 转成 Markdown

# 审查
/supermd 检查 docs/api.md 有什么问题

# 优化
/supermd 优化这份文档的排版

# 格式切换
/supermd 把这个文件从 Obsidian 转成 GFM
```

---

<p align="center">Made with ❤️ by <a href="https://github.com/Ruyi0623">星核网络工作室 (SparkCore)</a></p>
