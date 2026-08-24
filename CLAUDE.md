# CLAUDE.md

本文件为 Claude Code 提供此仓库的工作指引。

## 仓库概览

这是 **GitHub 个人主页 README** 仓库（`1byteone/1byteone`），在 `github.com/1byteone` 展示用户 GitHub 主页。**不是**应用项目，而是一个包含动态 SVG 资源、项目封面、架构图和 CI/CD 工作流的自包含 GitHub 主页。

配套 Hugo 博客站点位于 `/d/code/codeGithub/1byteone.github.io`（或 `/d/1byteone.github.io`）。

## 双仓库布局

| 仓库 | 用途 | 关键路径 |
|------|------|----------|
| **`fun-github-repo-profile`**（本仓库） | GitHub 主页 README — `1byteone/1byteone` | `README.md`, `assets/project-covers/`, `diagrams/`, `profile-3d-contrib/`, `repo-readmes/` |
| **`1byteone.github.io`** | HugoBlox 静态博客站点 — 38+ 篇技术文章，4 个精选项目 | `content/zh\|en/blog/`, `content/zh\|en/projects/`, `assets/media/` |

### 跨仓库图片操作

- **主页 README 项目封面** → `assets/project-covers/*.webp`（本仓库）— 1536×768 WebP，用于 README.md
- **博客/项目精选图** → `content/*/projects/*/featured.png`（1byteone.github.io）— 1200×630 PNG，Hugo 用作项目卡片缩略图
- **架构图** → `diagrams/*.svg`（本仓库）— 从 README 链接，同时在 1byteone.github.io 预览

## 精选项目（4 个）

| 项目 | 标识 | 描述 | README 锚点 |
|------|------|------|-------------|
| ruoyi-ai | `ruoyi-ai` | 企业级 AI 应用开发框架 | `#### 🏗️ ruoyi-ai` |
| ai-passage-creator | `ai-passage-creator` | AI 驱动的内容创作平台（灵犀写作） | `#### ✍️ ai-passage-creator` |
| mewpaw-code | `mewpaw-code` | Java 21 CLI Coding Agent | `#### 🤖 mewpaw-code` |
| zznursing | `zznursing` | 智颐智慧养老护理平台 | `#### 🏥 zznursing` |

每个项目包含：
- **封面图**：`assets/project-covers/{slug}-cover.webp`（1536×768）
- **中文 Hero 图**：`assets/project-covers/{slug}-hero-cn.webp`（1536×768）
- **机制说明图**：`assets/project-covers/material-illustrations/{slug}-material.webp`
- **架构 SVG 图**：`diagrams/{slug}-architecture.svg`
- **AI 生成提示词**：`assets/project-covers/prompts/*.md`
- **README 快照**：`repo-readmes/{slug}/README.md`

## README 结构

主页 README 是一个 `README.md` 文件，包含以下章节：

1. **简介 Banner** — 打字 SVG + 主页访问量徽章
2. **About Me** — 个人简介
3. **技术栈** — 后端 / AI & Agent / 工具徽章
4. **GitHub 统计** — 统计卡片、常用语言、连续贡献
5. **贡献图** — 活动图、贪吃蛇动画、3D 图表、活动流
6. **精选项目** — 4 个项目含封面图、Hero 图、机制说明图、架构图
7. **当前关注** — 当前工作状态
8. **联系我** — 邮箱

## CI/CD 工作流

| 工作流 | 文件 | 触发条件 | 执行动作 |
|--------|------|----------|----------|
| 3D 贡献图 | `.github/workflows/profile-3d.yml` | 每日 03:23 + push | 通过 `yoshi389111/github-profile-3d-contrib` 生成 `profile-3d-contrib/` SVG |
| 贪吃蛇动画 | `.github/workflows/snake.yml` | 每日 02:17 + push | 通过 `Platane/snk` 生成贪吃蛇 SVG，推送到 `output` 分支 |

## 资源流水线

### 封面图生成流程

1. **起草提示词** → `assets/project-covers/prompts/{id}-hero-{slug}.md`
2. **AI 图片生成** → 输出原始 `*-hero-cn-raw.webp`（或迭代版本 `*-raw-v2.webp`）
3. **缩放优化** → `ffmpeg` Lanczos 缩放到 1536×768 → `*-hero-cn.webp`
4. **机制说明图** → 独立提示词位于 `assets/project-covers/material-illustrations/prompts/`
5. **参考素材** → `assets/project-covers/references/`（Logo、品牌素材，用于提示词引导）

### 架构图流程

- SVG 源文件：`diagrams/{slug}-architecture.svg`
- HTML 渲染预览：`diagrams/{slug}-architecture.html`
- 预览 PNG：`.svg-previews/{slug}-architecture-*.png`

### 图片格式标准

| 场景 | 格式 | 尺寸 | 工具 |
|------|------|------|------|
| README 项目封面 | WebP | 1536×768 | `ffmpeg -vf "scale=1536:768:force_original_aspect_ratio=1,pad=1536:768:(ow-iw)/2:(oh-ih)/2" -quality 90` |
| 博客/项目精选图（1byteone.github.io） | PNG | 1200×630 | `ffmpeg -vf "scale=1200:630:force_original_aspect_ratio=1,pad=1200:630:(ow-iw)/2:(oh-ih)/2" -update 1 -frames:v 1 -quality 90` |
| 架构图 | SVG | 自适应 | PlantUML / 自定义 SVG |

## 常见操作

### 替换项目封面图

```bash
# 主页 README 封面（本仓库）
ffmpeg -y -i input.png -vf "scale=1536:768:force_original_aspect_ratio=1,pad=1536:768:(ow-iw)/2:(oh-ih)/2" -quality 90 -compression_level 6 assets/project-covers/{slug}-cover.webp

# 博客精选图（1byteone.github.io）
ffmpeg -y -i input.png -vf "scale=1200:630:force_original_aspect_ratio=1,pad=1200:630:(ow-iw)/2:(oh-ih)/2" -update 1 -frames:v 1 -quality 90 content/zh/projects/{slug}/featured.png
# 对 content/en/projects/{slug}/featured.png 重复此操作
```

### 添加新精选项目到 README

1. 添加封面图到 `assets/project-covers/`
2. 添加架构图到 `diagrams/`
3. 添加 README 快照到 `repo-readmes/{slug}/`
4. 按现有格式在 `README.md` 中添加项目章节
5. 更新 `assets/project-covers/prompts/` 生成提示词
6. 更新 `assets/project-covers/PROMPTS.md` 索引
7. （可选）添加机制说明图到 `assets/project-covers/material-illustrations/`

### 1byteone.github.io：添加新项目页面

1. 创建 `content/zh/projects/{slug}/index.md`，添加 frontmatter（featured: true, tech_stack, links, highlights）
2. 添加 `featured.png`（1200×630）
3. 对 `content/en/projects/{slug}/` 重复此操作
4. 确保 `featured: true` 以在首页展示

## Git 规范

- 分支：`master`
- 提交信息遵循常规提交规范：`feat:`、`fix:`、`chore:`、`refactor:`、`docs:`
- 3D 贡献图更新使用 `chore: update 3D contribution chart`
- `.gitignore` 排除项：`beautify-github-profile/`、`docs/`、`.tmp/`