# Frontend Slides

[English](README.en.md) · [原仓库 README](https://github.com/zarazhangrui/frontend-slides/blob/main/README.md)

Frontend Slides 是一个给本地 coding agent 使用的演示文稿生成 skill。它可以从零生成 HTML 演示，也可以把 PowerPoint 转成网页演示。产物默认是一个可携带文件夹：根目录 `index.html`，素材放在 `assets/`，可以压缩、发送、解压后直接打开。

## 这个仓库是什么

这个仓库是 [zarazhangrui/frontend-slides](https://github.com/zarazhangrui/frontend-slides) 的维护 fork。

原仓库提供了 Frontend Slides 的核心思路和基础能力：用 agent 生成高质量、零依赖、动画丰富的 HTML slides，并通过视觉预览帮助用户选择风格。

这个 fork 保留原项目方向，同时重点打磨：

- 更清晰的便携文件夹输出：`index.html` + 本地 `assets/`
- 生成 deck 内置的 Visual Deck Editor 运行时
- 更明确的 fork 安装、插件 metadata 和 agent 使用说明
- 更清楚的编辑器契约和维护边界

简单说：**原仓库是基础项目；这个 fork 是在基础项目之上继续打磨编辑器和便携交付体验。**

## 和原仓库的关系

- 原项目：[`zarazhangrui/frontend-slides`](https://github.com/zarazhangrui/frontend-slides)
- 当前 fork：[`wengzige/frontend-slides`](https://github.com/wengzige/frontend-slides)
- 原作者署名和 MIT License 保留
- 这个 fork 不把自己说成原始上游项目
- 和这个 fork 的生成流程、便携输出、内置编辑器运行时相关的改动优先进入这个 fork
- 更通用、适合所有 Frontend Slides 用户的改动，可以再单独考虑是否向上游提交

## Visual Deck Editor 到底是什么

Visual Deck Editor 是生成 deck 里内置的一套编辑器运行时能力。它不是一个单独应用，也不是 npm 包。

仓库里的 [`visual-editor/`](visual-editor/README.md) 目前是运行时契约文档目录，不是源码包。这个目录只有 README 是刻意的：它负责把编辑器支持什么、不支持什么、维护时要守住哪些边界写清楚。

当前实现关系是：

- 编辑器代码通过 Frontend Slides 的生成模板进入最终 `index.html`
- 具体实现指导在 `html-template.md` 和 plugin 内对应文件里
- `visual-editor/README.md` 说明运行时契约和维护边界

它支持的能力：

- 面向固定舞台 HTML deck，而不是某个具体生成文件
- 可以从普通 DOM 推断可编辑文本、图片、SVG/canvas、视觉块
- `data-editable`、`data-editable-media`、`data-editable-box` 只是增强提示，不是硬依赖
- 不需要 npm、后端、账号或云服务
- 保存时会清理编辑器 UI、临时标记和选择框，让 `index.html` 保持可携带

它不声称支持：

- 通用网站编辑器
- 独立在线编辑产品
- npm 包式安装
- 任意网页结构
- 精确 PowerPoint 动画还原

## 安装

### Claude Code 插件安装

```text
/plugin marketplace add https://github.com/wengzige/frontend-slides
```

安装 marketplace 后再运行：

```text
/plugin install frontend-slides@frontend-slides
```

使用：

```text
/frontend-slides:frontend-slides
```

### 手动安装 skill

```bash
mkdir -p ~/.claude/skills/frontend-slides/scripts
cp SKILL.md STYLE_PRESETS.md viewport-base.css html-template.md animation-patterns.md ~/.claude/skills/frontend-slides/
cp -R bold-template-pack visual-editor ~/.claude/skills/frontend-slides/
cp scripts/extract-pptx.py scripts/deploy.sh scripts/export-pdf.sh ~/.claude/skills/frontend-slides/scripts/
```

也可以直接 clone：

```bash
git clone https://github.com/wengzige/frontend-slides.git ~/.claude/skills/frontend-slides
```

## 基本使用

新建演示：

```text
/frontend-slides:frontend-slides

> I want to create a pitch deck for my AI startup
```

转换 PowerPoint：

```text
/frontend-slides:frontend-slides

> Convert my presentation.pptx to a web slideshow
```

生成后，演示文件夹里会有 `index.html`。打开后可以按 `E` 进入编辑模式，修改文字、图片、形状、字体、布局和部分入场动效，然后保存为干净的 HTML。

## 主要文件

- `SKILL.md`：agent 执行这个 skill 的核心说明
- `html-template.md`：HTML deck 和编辑器的模板/契约说明
- `viewport-base.css`：固定 16:9 舞台的基础 CSS
- `bold-template-pack/`：可选视觉模板
- `visual-editor/`：Visual Deck Editor 的运行时契约和维护边界
- `plugins/frontend-slides/`：Claude Code plugin 包装

## Credits

Originally created by [@zarazhangrui](https://github.com/zarazhangrui).

This fork is maintained by [@wengzige](https://github.com/wengzige).

## License

MIT
