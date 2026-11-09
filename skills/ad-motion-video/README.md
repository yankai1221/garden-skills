# ad-motion-video

制作竖版信息流短视频广告的 Agent Skill（Claude Code、Codex 等支持 Agent Skills 格式的智能体都能用）：数字人出镜加代码画面，四页七句结构，带拆片、风格库、相似度预检和成片验收。用法见 `SKILL.md`。

## 来源和许可证

- 改编自 [ConardLi/garden-skills](https://github.com/ConardLi/garden-skills) 的 `skills/motion-showreel`（版本 0.2.0，commit `08150e750bdc8c8dc452fb43c8ef5221b71c4308`，2026-11-08）。
- 原作者：ConardLi。原项目和本改编都使用 MIT 许可证，原许可证全文见本目录 `LICENSE`。
- `scripts/`、`assets/`、`references/`（除下面列出的新增和改动外）来自原 Skill，保留原样。

## 相对原版改了什么

| 类别 | 内容 |
|---|---|
| 重写 | `SKILL.md`：默认用途改成竖版信息流广告（1080×1920、25～35 秒），默认四页七句结构；加入广告审核硬规则、素材相似度预检、配音试听、数字人花钱请示；工作流加入「骨架关键帧 + 相似度预检」和「配音试听」两个停点 |
| 新增 | `references/feed-ad.md`：七个槽位、四页版式要点、一条样片的实测节奏数据、裂变时保留和必换的项、相似度预检方法 |
| 新增 | `local/` 机制：使用者把自己的禁用词、产品口径、价格、音色、形象、路径和审批规则放在 `local/`，SKILL.md 要求先读；`local/` 被 `.gitignore` 排除，不公开 |
| 修改 | `scripts/inspect.mjs`：Windows 上 ffmpeg 的 drawtext 走 fontconfig 会崩溃，改为默认传 `C:/Windows/Fonts/arial.ttf`，可用环境变量 `INSPECT_FONTFILE` 覆盖 |
| 修改 | `scripts/package-lock.json`：原锁文件的下载地址是一个内部镜像，改为从 npm 官方源重新生成 |
| 去掉 | 对 `web-video-presentation`、`web-design-engineer` 的引用（横版演示和网页设计，与竖版广告无关）；原版 README 和 manifest |
| 降级 | 20 分钟长片（`references/long-form.md`、`scripts/build-long.mjs`）保留，但不再是默认用途 |

## 依赖

Node 18+、ffmpeg（含 ffprobe）。在 `scripts/` 里 `npm install`，再 `npx playwright install chromium`，然后 `node check-env.mjs`。`node_modules/` 不进版本库。
