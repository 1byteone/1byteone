# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is the **GitHub Profile README** repository (`1byteone/1byteone`) — it renders as the user's GitHub profile page at `github.com/1byteone`. It is **not** an application project; it is a self-contained GitHub profile with dynamically generated SVG assets, project covers, architecture diagrams, and CI/CD workflows.

A companion Hugo blog site lives at `/d/code/codeGithub/1byteone.github.io` (or `/d/1byteone.github.io`).

## Two-Repo Landscape

| Repo | Purpose | Key Paths |
|------|---------|-----------|
| **`fun-github-repo-profile`** (this repo) | GitHub Profile README — the `1byteone/1byteone` repo | `README.md`, `assets/project-covers/`, `diagrams/`, `profile-3d-contrib/`, `repo-readmes/` |
| **`1byteone.github.io`** | HugoBlox static blog site — 38+ tech blog posts, 4 featured projects | `content/zh\|en/blog/`, `content/zh\|en/projects/`, `assets/media/` |

### Image Operations Across Repos

- **Profile README covers** → `assets/project-covers/*.webp` (this repo) — 1536×768 WebP, used in README.md
- **Blog/Project featured images** → `content/*/projects/*/featured.png` (1byteone.github.io) — 1200×630 PNG, used by Hugo as project card thumbnails
- **Architecture diagrams** → `diagrams/*.svg` (this repo) — linked from README, also previewed in 1byteone.github.io

## Featured Projects (4)

| Project | Slug | Description | README Anchor |
|---------|------|-------------|---------------|
| ruoyi-ai | `ruoyi-ai` | 企业级 AI 应用开发框架 | `#### 🏗️ ruoyi-ai` |
| ai-passage-creator | `ai-passage-creator` | AI 驱动的内容创作平台（灵犀写作） | `#### ✍️ ai-passage-creator` |
| mewpaw-code | `mewpaw-code` | Java 21 CLI Coding Agent | `#### 🤖 mewpaw-code` |
| zznursing | `zznursing` | 智颐智慧养老护理平台 | `#### 🏥 zznursing` |

Each project has:
- **Cover image**: `assets/project-covers/{slug}-cover.webp` (1536×768)
- **Chinese Hero**: `assets/project-covers/{slug}-hero-cn.webp` (1536×768)
- **Material illustration**: `assets/project-covers/material-illustrations/{slug}-material.webp`
- **Architecture SVG**: `diagrams/{slug}-architecture.svg`
- **AI generation prompts**: `assets/project-covers/prompts/*.md`
- **README snapshot**: `repo-readmes/{slug}/README.md`

## README Structure

The profile README is a single `README.md` file with these sections:

1. **Intro Banner** — Typing SVG + profile views badge
2. **About Me** — Brief bio
3. **Tech Stack** — Backend / AI & Agent / Tools badges
4. **GitHub Stats** — Stats cards, top languages, streak
5. **Contribution Graph** — Activity graph, snake animation, 3D chart, activity flow
6. **Featured Projects** — 4 projects with cover images, hero images, material illustrations, architecture SVGs
7. **Currently Focus** — Current work status
8. **Get in Touch** — Email contact

## CI/CD Workflows

| Workflow | File | Trigger | Action |
|----------|------|---------|--------|
| 3D Contribution Chart | `.github/workflows/profile-3d.yml` | Daily 03:23 + push | Generates `profile-3d-contrib/` SVGs via `yoshi389111/github-profile-3d-contrib` |
| Snake Animation | `.github/workflows/snake.yml` | Daily 02:17 + push | Generates snake SVG via `Platane/snk`, pushes to `output` branch |

## Asset Pipeline

### Cover Image Generation Workflow

1. **Draft prompt** → `assets/project-covers/prompts/{id}-hero-{slug}.md`
2. **Generate via AI image** → output raw `*-hero-cn-raw.webp` (or `*-raw-v2.webp` for iterations)
3. **Resize & optimize** → `ffmpeg` Lanczos resize to exact 1536×768 → `*-hero-cn.webp`
4. **Material illustration** → separate prompt in `assets/project-covers/material-illustrations/prompts/`
5. **Reference materials** → `assets/project-covers/references/` (logos, brand assets for prompt guidance)

### Architecture Diagram Workflow

- SVG source: `diagrams/{slug}-architecture.svg`
- Rendered HTML viewer: `diagrams/{slug}-architecture.html`
- Preview PNGs: `.svg-previews/{slug}-architecture-*.png`

### Image Format Standards

| Context | Format | Size | Tool |
|---------|--------|------|------|
| README project covers | WebP | 1536×768 | `ffmpeg -vf "scale=1536:768:force_original_aspect_ratio=1,pad=1536:768:(ow-iw)/2:(oh-ih)/2" -quality 90` |
| Blog/project featured (1byteone.github.io) | PNG | 1200×630 | `ffmpeg -vf "scale=1200:630:force_original_aspect_ratio=1,pad=1200:630:(ow-iw)/2:(oh-ih)/2" -update 1 -frames:v 1 -quality 90` |
| Architecture diagrams | SVG | responsive | PlantUML / custom SVG |

## Common Operations

### Replace a Project Cover Image

```bash
# Profile README cover (this repo)
ffmpeg -y -i input.png -vf "scale=1536:768:force_original_aspect_ratio=1,pad=1536:768:(ow-iw)/2:(oh-ih)/2" -quality 90 -compression_level 6 assets/project-covers/{slug}-cover.webp

# Blog featured image (1byteone.github.io)
ffmpeg -y -i input.png -vf "scale=1200:630:force_original_aspect_ratio=1,pad=1200:630:(ow-iw)/2:(oh-ih)/2" -update 1 -frames:v 1 -quality 90 content/zh/projects/{slug}/featured.png
# Repeat for content/en/projects/{slug}/featured.png
```

### Add a New Featured Project to README

1. Add cover images to `assets/project-covers/`
2. Add architecture diagram to `diagrams/`
3. Add README snapshot to `repo-readmes/{slug}/`
4. Add project section in `README.md` following existing pattern
5. Update `assets/project-covers/prompts/` with generation prompts
6. Update `assets/project-covers/PROMPTS.md` index
7. (Optional) Add material illustration to `assets/project-covers/material-illustrations/`

### 1byteone.github.io: Add a New Project Page

1. Create `content/zh/projects/{slug}/index.md` with frontmatter (featured: true, tech_stack, links, highlights)
2. Add `featured.png` (1200×630)
3. Repeat for `content/en/projects/{slug}/`
4. Ensure `featured: true` for it to appear on the homepage

## Git Conventions

- Branch: `master`
- Commit messages follow conventional commits: `feat:`, `fix:`, `chore:`, `refactor:`, `docs:`
- 3D contribution chart updates use `chore: update 3D contribution chart`
- `.gitignore` excludes: `beautify-github-profile/`, `docs/`, `.tmp/`