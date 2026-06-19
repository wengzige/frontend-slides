# Frontend Slides

[English](README.en.md) · [原仓库 README](https://github.com/zarazhangrui/frontend-slides/blob/main/README.md)

**从想法或 PPT 生成漂亮 HTML 演示，然后直接在浏览器里改文字、换图片、调布局。**

Frontend Slides 是一个给本地 coding agent 使用的演示文稿生成 skill。它可以从零生成 HTML 演示，也可以把 PowerPoint 转成网页演示。和普通“导出成 HTML”不同：生成后的 `index.html` 自带可视化编辑模式，打开后按 `E` 就能继续修改，并保存为干净、可携带的 HTML deck。

## 为什么编辑器值得注意

- **生成后还能继续改**：不是一次性静态页面，打开 `index.html` 就能进入编辑模式。
- **直接改真实演示稿**：可编辑文字、替换图片、调整形状、字体、布局和部分入场动效。
- **不用额外安装东西**：不需要 npm、后端、账号或云服务，压缩发给别人也能打开。
- **保存结果干净**：保存时清理编辑器 UI、选择框和临时标记，仍然是普通可分享的 HTML 文件夹。

## 这个仓库是什么

这个仓库是 **@wengzige 独立维护的 Frontend Slides 版本**。它基于 [zarazhangrui/frontend-slides](https://github.com/zarazhangrui/frontend-slides) 的 MIT 开源基础继续开发，但不是把上游仓库原样复制一份。

原仓库提供了 Frontend Slides 的核心思路和基础能力：用 agent 生成高质量、零依赖、动画丰富的 HTML slides，并通过视觉预览帮助用户选择风格。

这个版本继续保留原项目方向，同时把重点放在实际使用体验上：

- 更清晰的便携文件夹输出：`index.html` + 本地 `assets/`
- 生成后的演示文稿自带可视化编辑模式，按 `E` 就能继续改
- 编辑器可处理文字、图片、视觉块、字体、布局和部分入场动效
- 保存时清理编辑器 UI 和临时标记，让结果仍然是干净的 HTML deck
- 更明确的 Claude Code 插件安装、metadata 和 agent 使用说明
- 更清楚的编辑器运行时契约和维护边界

简单说：**原仓库是基础项目；这个仓库是围绕“生成后还能继续编辑、能打包交付、能让 agent 稳定复用”的独立维护版本。**

## 这个版本具体做了什么

- **把生成结果从单个页面思路打磨成便携项目文件夹**：根目录 `index.html`，媒体资源放进本地 `assets/`，方便压缩、发送、解压后直接打开。
- **加入并持续打磨 Visual Deck Editor**：生成后的 deck 可以在浏览器里进入编辑模式，继续改文字、图片、形状、字体、布局和部分动效。
- **把编辑器做成固定运行时，而不是每套 deck 临时生成一份**：`visual-editor/` 维护统一的 `editor-runtime.css` 和 `editor-runtime.js`，减少一次性代码和行为漂移。
- **补齐 agent 可执行的生成契约**：`html-template.md`、`SKILL.md`、`visual-editor/README.md` 明确说明固定舞台、编辑器挂载、保存清理和运行时边界。
- **整理插件安装和公开仓库说明**：让这个仓库可以作为 Claude Code plugin/skill 来源使用，而不是只停留在实验代码状态。
- **整合更大胆的视觉模板选择流程**：`bold-template-pack/` 提供可选风格系统，同时保持渐进读取，避免让 agent 一次性吃掉所有模板上下文。

## 和原仓库的关系

- 原项目：[`zarazhangrui/frontend-slides`](https://github.com/zarazhangrui/frontend-slides)
- 当前独立维护版：[`wengzige/frontend-slides`](https://github.com/wengzige/frontend-slides)
- 原作者署名和 MIT License 保留
- 这个仓库不把自己说成原始上游项目，也不抹掉原项目贡献
- 和这个版本的生成流程、便携输出、内置编辑模式相关的改动优先进入这个仓库
- 更通用、适合所有 Frontend Slides 用户的改动，可以再单独考虑是否向上游提交

## Visual Deck Editor 到底是什么

Visual Deck Editor 是写进生成后 `index.html` 里的浏览器编辑模式。它不是一个单独应用，也不是 npm 包。

仓库里的 [`visual-editor/`](visual-editor/README.md) 是固定编辑器运行时目录。生成 deck 时要复制里面的 `editor-runtime.css` 和 `editor-runtime.js`，不要让 agent 给每套 deck 临时写一个新编辑器。

当前实现关系是：

- 编辑器运行时代码在 `visual-editor/editor-runtime.css` 和 `visual-editor/editor-runtime.js`
- 生成模板在 `html-template.md` 里说明如何从 `index.html` 挂载这套固定运行时
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
- `visual-editor/`：Visual Deck Editor 的固定运行时、运行时契约和维护边界
- `plugins/frontend-slides/`：Claude Code plugin 包装

## Credits

Originally created by [@zarazhangrui](https://github.com/zarazhangrui).

This independently maintained version is developed by [@wengzige](https://github.com/wengzige), with substantial work on portable output, the built-in Visual Deck Editor, plugin packaging, and agent-facing runtime documentation.

## License

MIT
