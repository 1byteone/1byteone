# 归藏材料插画补图

这组三张补图使用 `guizang-material-illustration` 的材料化解释图方法，
并由 `$gpt-image` 生成。它们用于补充项目机制，不替代 README 当前使用的
深色 Hero 封面。

## 统一规范

- 画布：2:1 横向，正式资产 `1536x768`。
- 风格：3D Swiss editorial material illustration。
- 背景：暖灰纸张底，保留充足留白与 80px 安全边距。
- 材质：哑光树脂、折叠纸张、磨砂金属、半透明亚克力。
- 信息：一个核心结构，3-5 个主要短标签，避免长段落与密集图例。
- 中文：仅显示提示词指定的简体中文，清晰、准确、无乱码。
- 禁止：仪表盘、网页截图、卡片墙、伪代码、微型正文、随机品牌、
  通用机器人、装饰光球、赛博城市、水印与边框。

## 提示词与资产

| 项目 | 概念结构 | 提示词 | 正式资产 |
|---|---|---|---|
| ruoyi-ai | 企业 AI 中枢与五类能力 | `prompts/01-ruoyi-ai-material.md` | `ruoyi-ai-material.webp` |
| ai-passage-creator-demo | 多智能体内容创作流水线 | `prompts/02-ai-passage-creator-material.md` | `ai-passage-creator-material.webp` |
| mewpaw-code | ReAct 循环、六工具、五层防护 | `prompts/03-mewpaw-code-material.md` | `mewpaw-code-material.webp` |

`*-material-raw.webp` 保留 `$gpt-image` 原始输出；正式资产经过高质量
缩放，统一为精确的 `1536x768`。
