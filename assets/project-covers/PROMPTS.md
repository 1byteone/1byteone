# 项目封面提示词

这些新增中文 Hero 用于 `1byteone/1byteone` GitHub Profile 的
Featured Projects 区域，同时兼顾 README Hero 与 GitHub Social Preview
的缩略图阅读体验。仓库原始封面完整保留，两套视觉在 README 中共存。

## 新增 Hero 规范

- 正式画布：2:1 横向，`1536x768`。
- 格式：高质量、不透明 WebP。
- 构图：左侧项目名称、中文定位与能力摘要，右侧一个可识别的项目主符号。
- 层级：项目名称最大，中文定位第二，能力标签与技术栈第三。
- 风格：深色编辑视觉、克制的技术网格、精密材料与工作室光照。
- 中文：仅使用准确的简体中文，字形清晰，无乱码、错别字或拼音。
- 缩略图：在 GitHub README 宽度缩小时仍能读出项目名与一句核心定位。
- 禁止：仪表盘截图、密集微型 UI、真人、通用机器人头、随机品牌、
  无意义代码、赛博城市、过量霓虹、版权角色与水印。

## 可复现提示词

四张正式封面的完整提示词分别保存在：

- [`prompts/01-hero-ruoyi-ai.md`](prompts/01-hero-ruoyi-ai.md)
- [`prompts/02-hero-ai-passage-creator.md`](prompts/02-hero-ai-passage-creator.md)
- [`prompts/03-hero-mewpaw-code.md`](prompts/03-hero-mewpaw-code.md)
- [`prompts/04-hero-zznursing.md`](prompts/04-hero-zznursing.md)

这些文件记录项目事实、精确中文文案、品牌符号、构图、材质、配色、
禁止项与输出规格。重新生成时以对应文件为唯一提示词来源。

## 资产分层

### 原始封面

以下仓库原图保持原文件名和原始内容不变：

- `ruoyi-ai-cover.webp`
- `ai-passage-creator-cover.webp`
- `mewpaw-code-cover.webp`
- `zznursing-cover.webp`

### 新增中文 Hero

- `ruoyi-ai-hero-cn.webp`
- `ai-passage-creator-hero-cn.webp`
- `mewpaw-code-hero-cn.webp`
- `zznursing-hero-cn.webp`

`*-hero-cn-raw.webp` 是 `$gpt-image` 输出的原始母版；新增正式 Hero
经过 Lanczos 高质量缩放，统一为精确的 `1536x768`。

## zznursing 迭代说明

- `zznursing-hero-cn-raw.webp`：首版草稿，因加入额外数字信息与微文案而弃用。
- `zznursing-hero-cn-raw-v2.webp`：修订后接受母版。
- `zznursing-hero-cn.webp`：基于接受母版导出的正式 README / Social Preview 版本。

## 补充机制图

四个项目另有一套基于 `guizang-material-illustration` 的浅色 3D Swiss
材料解释图，用于展示架构、流程与安全机制。提示词、原始母版与正式资产
见 [`material-illustrations/PROMPTS.md`](material-illustrations/PROMPTS.md)。
