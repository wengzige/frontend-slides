# Frontend Slides 中文说明

[English](README.md)

Frontend Slides 是一个给本地 coding agent 使用的演示文稿生成 skill。它可以从零生成 HTML 演示，也可以把 PowerPoint 转成网页演示。产物默认是一个可携带文件夹：根目录 `index.html`，素材放在 `assets/`，可以压缩、发送、解压后直接打开。

## 这个仓库是什么

这个仓库是 [zarazhangrui/frontend-slides](https://github.com/zarazhangrui/frontend-slides) 的维护 fork。

原仓库提供了 Frontend Slides 的核心思路和基础能力：用 agent 生成高质量、零依赖、动画丰富的 HTML slides，并通过视觉预览帮助用户选择风格。

这个 fork 继续保留原项目的方向，同时重点维护几类增强：

- 更清晰的便携文件夹输出：`index.html` + 本地 `assets/`
- 更实用的 Visual Deck Editor
- 更明确的 fork 安装、插件 metadata 和 agent 使用说明
- 以后可能把编辑器逐步抽成独立项目

## 和原仓库的关系

- 原项目：[`zarazhangrui/frontend-slides`](https://github.com/zarazhangrui/frontend-slides)
- 当前 fork：[`wengzige/frontend-slides`](https://github.com/wengzige/frontend-slides)
- 原作者署名和 MIT License 保留
- 这个 fork 不把自己说成原始上游项目
- 和 Visual Deck Editor 孵化路线相关的改动优先进入这个 fork
- 更通用、适合所有 Frontend Slides 用户的改动，可以再单独考虑是否向上游提交

简单说：**原仓库是基础项目；这个 fork 是在基础项目之上继续打磨编辑器和便携交付体验。**

## Visual Deck Editor 独立到什么程度

编辑器已经不是单个 deck 的一次性脚本。它现在有自己的文档目录：

[`visual-editor/`](visual-editor/README.md)

它目前相对独立的部分：

- 面向通用固定舞台 HTML deck，而不是某个具体生成文件
- 可以从普通 DOM 推断可编辑文本、图片、SVG/canvas、视觉块
- `data-editable`、`data-editable-media`、`data-editable-box` 只是增强提示，不是硬依赖
- 不需要 npm、后端、账号或云服务
- 保存时会清理编辑器 UI、临时标记和选择框，让 `index.html` 保持可携带

它目前还没有完全独立的部分：

- 仍然通过 Frontend Slides 生成流程内置到 deck 里
- 默认依赖固定舞台结构：`#deckStage` 或 `.deck-stage`、`.slide`、1920x1080 坐标
- 还没有单独 npm 包、稳定 public API、独立 demo 矩阵或浏览器回归测试

所以当前最佳路线是：**先在这个 fork 内作为一等模块孵化，等 API、demo 和测试稳定后，再拆成独立 GitHub 仓库。**

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
- `visual-editor/`：Visual Deck Editor 的模块边界和拆分路线
- `plugins/frontend-slides/`：Claude Code plugin 包装

## Credits

Originally created by [@zarazhangrui](https://github.com/zarazhangrui).

This fork is maintained by [@wengzige](https://github.com/wengzige).

## License

MIT
