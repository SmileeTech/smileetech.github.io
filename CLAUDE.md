# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 部署与本地预览

无构建步骤、无依赖、无测试、无 lint。这是纯静态的 HTML + CSS 站点。

- **部署**：GitHub Pages，仓库即站点（`SmileeTech/smileetech.github.io`，`main` 分支 = 生产环境）。推送 `main` 即上线。
- **自定义域名**：`dev.smileetechnology.com`，由根目录 `CNAME` 文件声明——不要删除或重命名它。
- **本地预览**：在仓库根目录用任意静态服务器即可，例如 `python3 -m http.server 8000`，然后访问 `http://localhost:8000`。

## 架构

单页站点，全部代码就两个文件加一个 `img/` 目录：

- `index.html` —— 唯一页面。
- `css/reset.css` —— CSS reset（47 行）。
- `css/main.css` —— 全部业务样式（约 714 行）。

关键技术约束（改动前需要知道）：

- **布局用老式 `float` + `.clearfix`**（`.float--left` / `.float--right`）。`main.css` 里没有任何 `@media` 查询——README 明确这是 V1.0 的 desktop-only 版本，**当前不支持响应式**。要做响应式需要从头重构布局方式。
- **主题色 `#7449D8`（紫色）硬编码**散落在 `main.css` 各处（背景、边框、SVG fill 等），**没有 CSS 变量 / token**。换主色必须全局搜索替换 `#7449D8`。
- **字体** Poppins（多种字重）+ Bebas Neue，通过 `index.html` `<head>` 中多个 `<link>` 从 Google Fonts 加载——改字体在那里改。
- **分隔线**（section 之间的波浪形）是内联 SVG，类名形如 `custom-shape-divider-*`（带原始时间戳后缀，来自生成器工具）。
- **"Hire Us" 区的表单是纯展示**：`<input>` 和 `<input type="submit">` 没有绑定任何后端 / 表单处理，提交不会发到任何地方。要让它工作需要自己接后端。

## 品牌迁移（进行中）

站点源自第三方模板（原作者的 "team-website-template" / "Auroraim build team"，2021 年）。标题已改为 **Smilee Technology**，但**品牌迁移尚未完成**——以下位置仍残留原模板的 "Auroraim" 字样，编辑时留意是否需要一并替换：

- `<meta>` / Open Graph 描述（`index.html` `<head>`）
- "Who are we?" 段落正文与署名
- `<footer>` 的 credits / socials

`README.md` 是原模板作者写的说明，描述的是模板用途，与当前品牌和实际功能并不完全一致，参考时请以代码为准。

## app-ads.txt

根目录 `app-ads.txt` 用于移动应用广告（AdSense / Authorized Digital Sellers）授权，列出了多个 Google publisher ID（`pub-...`）。这是站点的一个实际功能用途，最近几次提交都在更新它。**改动或删除其中的行会影响广告授权，除非明确要求否则不要动。**
