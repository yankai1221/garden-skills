---
name: ad-motion-video
description: 制作竖版信息流短视频广告（默认 1080×1920、25～35 秒，例如视频号、抖音信息流）：数字人出镜加代码画面，按「价值对比钩子 → 安装或使用步骤 → 卖点墙 → 价格」四页结构出片；带拆参考片节奏（剪点、节拍、运动热图）、40 多种画面风格库、同账户素材相似度预检、成片技术验收。用户说「做一条信息流广告」「裂变一条爆款素材」「拆一下这条广告的节奏」「换个风格重做这条广告」「广告成片验收」时使用。不用于长视频、横版演示、写实人物生成。
---

# 竖版信息流广告视频（ad-motion-video）

把一份已审核的口播稿做成竖版信息流广告：真人或数字人只在开头和结尾出镜，中间用代码做的画面讲清「怎么得到」「为什么放心」，最后给价格。交付 MP4 和能重建的源码。

本 Skill 改编自 motion-showreel（MIT），保留了它的渲染管线、风格库、手法库、拆片和验收工具，把默认用途改成信息流广告，并加入广告审核和素材相似度两道关。来源和改动见 `README.md`。

## 第一件事：读本地规矩

**如果本目录下有 `local/` 文件夹，先把里面的文件全部读完，再做任何事。** `local/` 放的是使用者自己的规矩（禁用词、产品口径、价格、配音音色、数字人形象、本机路径、花钱审批），不公开。`local/` 和本文件冲突时，以 `local/` 为准。

没有 `local/` 时，按本文件的通用规则做，所有产品事实、价格、禁用词都向用户问清楚，不自己编。

## 默认规格

| 项 | 默认 | 说明 |
|---|---|---|
| 画幅 | 竖版 1080×1920，30 帧 | 用户另行指定时照用户的 |
| 时长 | 25～35 秒 | 以口播实际长度为准，不为凑时长变速或截断 |
| 用途 | 信息流广告，点击后进商品页 | 结尾要有明确的价格和行动口播 |
| 结构 | 四页七句（见下） | `references/feed-ad.md` 有逐句槽位和时长比例 |
| 人物 | 数字人或真人片段 + 代码画面 | `references/formats.md` 的 H 类；数字人一般是付费服务 |
| 长片 | 不默认 | 超过 2 分钟的讲解片仍可按 `references/long-form.md` 做，但不是本 Skill 的主要用途 |

## 默认结构：四页七句

| 页 | 句 | 作用 | 画面 | 参考时长 |
|---|---|---|---|---|
| ① 钩子页 | 1 | 价值对比：「[熟悉的东西] 只会 [旧结果]，[产品] 能直接 [新结果]」 | 真人正脸，0 秒开口；旧做法卡弱、新做法卡强，产品名在后半句亮出 | 约 4.5 秒 |
| ② 步骤页 | 2–3 | 过渡到「先装好 / 先用上」，再讲怎么装：几步、多快、产品专属加分项 | 无真人；步骤逐个完成（打勾、填进度） | 约 8 秒 |
| ③ 卖点墙 | 4–5 | 打消顾虑：正不正规、能不能用、贵不贵、装不上怎么办 | 无真人；每说一个短语出一个标签 | 约 10 秒 |
| ④ 价格页 | 6–7 | 价格 + 行动口播 | 真人回来；大号价格数字，小字产品名，一句行动短语 | 约 4 秒 |

- 整片只换 3 次页，页内靠「每说一个短语出一个元素」制造节奏（约每秒一个）。
- 真人出镜合计不超过 10 秒，只放在钩子、价格、行动这几句。
- 画面下沿约 1650～1920 像素留空：信息流的标题、按钮、头像会压在这里。
- 这是默认骨架，不是唯一结构。口播稿结构不同时，按稿件来，但先在 brief 里写明偏离了哪里、为什么。

## 广告审核硬规则（所有风格都要守）

以下是通用规则；具体的禁用词、产品口径和平台规定写在 `local/`。

1. **开头不打招呼、不自我介绍**：第一句直接是产品加痛点、对比、结果或反常点。
2. **画面里不出现任何网址、二维码**；不出现 `local/` 里列出的禁用品牌名和词。
3. **点击类文字不上屏**（如「点击下方链接购买」），口播可以说。
4. **系统支持范围只说实际支持的**，不暗示支持没测过的平台。
5. **产品专属功能不跨产品**：只有 A 产品有的功能，B 产品的视频里不能出现。
6. **不提账号、密钥、令牌、注册流程、官网这类词**，除非 `local/` 明确允许。
7. **不做虚假承诺**：功能、数字、价格只来自用户或可靠资料，不确定的标出来问。
8. **真实录屏只裁局部**：不露网址、第三方软件图标、含「点击」的弹窗和日志行。
9. 每一页的文字都要在手机尺寸下看得清，停留够读完（`references/craft.md` 第 7 节）。

## 素材相似度：交付前必须比

信息流平台会把同一账户里的视频互相比较，画面大部分相同会被拒。只换文案或配音不够，只做镜像、裁切、调色有被判为规避审核的风险。

- **骨架阶段先比**：用占位素材渲出每一页的关键帧，和账户里所有已上传视频对比，不像了再配音、再花钱做数字人。
- **交付前整条再比一次**：和已上传视频、同批其他条都比。
- 用项目自己的相似度工具（`local/` 写了用哪个）；没有时用感知哈希加 SSIM，方法和备用命令见 `references/feed-ad.md`「相似度预检」。
- 拉开相似度靠换**大块明暗分布和构图**：分屏几何、底色明暗、中段两页的版式、人物裁切、价格页构图。风格库就是干这个的：同一条口播，换一个风格（`references/styles/INDEX.md`）就是换一整套画面语言。
- 保留优秀素材的**画面逻辑**（前 3 秒画面类型、痛点怎么展示、转化镜头的类型），不复用原画面。

## 配音

- 口播稿必须是已经审核过的定稿，本 Skill 不代写、不改写后擅自合成。
- 用读音替换表修正读错的词时，**替换表只给会读错的那个 TTS 引擎用**；换了引擎，直接写原词，再试听确认。字幕和画面始终显示原词。
- 同一条视频不混用两家 TTS 的声音。
- 合成后先自动核对（总时长和字数是否相称、段间停顿数是否等于段数减一，对不上多半是重复念或漏念），**然后每条音频都要人工试听确认**，确认后才能做数字人和出片。
- 产品名这类容易读错的词，把每一处截出来给人重点听；转写核对查不出读音错。
- 引擎、音色、语气写法见 `references/narration.md`；使用者自己的音色和替换表在 `local/`。

## 数字人片段（H 类：人物 + 代码场景）

- 数字人通常是付费接口。**每次调用前先请示**（谁审批写在 `local/`），调用前后都查余额并记账。
- 只把要出镜的那几句从整条配音里剪出来（前后各留约 0.2 秒），用音频驱动口型，各段分开生成，不拼成一条。
- 有绿幕时按 `references/formats.md` H 类抠像合成；没有绿幕（照片形象自带背景）时直接放进代码画面的框里，框的几何形状就是拉开相似度的关键之一。
- 版式要和账户里已用过的出镜版式不同（上人下字、圆形小窗、左右分屏、斜切分屏等，`local/` 里有已用清单）。

## 工作流

```
0 环境检查（一次）
1 需求确认 ──── 产品、卖点、口播定稿、数字人与否、参考素材、已上传视频清单 → 🛑 等用户确认
2 拆参考 + brief ── inspect 量节奏 → 四页分镜 → 选风格（避开已用版式）
3 骨架关键帧 ──── 占位素材渲每页关键帧 → 相似度预检 → 🛑 等用户确认方向
4 配音 ──────── 合成 → 自动核对 → 🛑 人工试听确认
5 数字人 ─────── 🛑 请示花钱 → 剪出镜句 → 生成 → 记账
6 制作 ──────── timeline → 逐页 → 静帧和连续帧自查 → 确定性检查
7 预览 ──────── 工作区预览 → 🛑 确认导出
8 导出与验收 ──── qa 技术检查 + 审核硬规则自查 + 相似度终检 + 审片
9 交付 ──────── 成片进待审批位置（见 local/），不直接投放
```

### 第 0 步：环境

第一次使用：在 `scripts/` 里运行 `npm install`（Playwright 和 Tone.js），再运行 `npx playwright install chromium`，然后 `node scripts/check-env.mjs`。需要 Node 18+ 和 ffmpeg（含 ffprobe），缺了告诉用户怎么装，不替用户装系统软件。Git Bash / macOS / Linux 也可以用 `sh scripts/setup.sh`。工具自带测试：`cd scripts && npm test`。

Windows 提示：有的 ffmpeg 版本没配好 fontconfig，带时间戳的拼图会崩溃；本 Skill 的 `inspect.mjs` 在 Windows 上默认用 `C:/Windows/Fonts/arial.ttf`，也可以设环境变量 `INSPECT_FONTFILE` 指定字体文件。

### 第 1 步：需求确认（停下来等用户）

必须明确，不能用默认值代替用户决定：

| 必填 | 说明 |
|---|---|
| 产品和卖点清单 | 只用用户给的或可靠资料里的说法 |
| 口播定稿 | 已经过审核的定稿；不代写 |
| 时长、画幅 | 默认 25～35 秒、1080×1920，写进摘要让用户确认 |
| 数字人 | 用不用、用哪个形象、谁批准花钱 |
| 配音 | 引擎、音色，是否已有试听通过的音频 |
| BGM、音效 | AI 合成 / 用户提供 / 关闭，分开选 |
| 参考素材 | 要学节奏的爆款或对标视频 |
| 已上传视频 | 相似度对比要用的视频目录 |

汇总成摘要，**停下来等用户确认**。

### 第 2 步：拆参考 + brief

有参考视频时先量，把数字写进 brief 的对标一栏（只学结构和节奏，不搬素材）：

```bash
node scripts/inspect.mjs sheet <ref> --cells 30 --out <qa>/ref       # 总览图
node scripts/inspect.mjs grid  <ref> --strips --out <qa>/ref         # 剪点 + 节拍网格 + 转场连续帧
node scripts/inspect.mjs heat  <ref> --out <qa>/ref                  # 每段哪里在动、动多大面积
node scripts/inspect.mjs qa    <ref> --out <qa>/ref-qa --expect-size 1080x1920 --expect-fps 30 --expect-duration <秒> --audio required --timeline none
```

然后按 `references/brief-template.md` 写 brief，Reel Read 里 `format` 写「信息流广告（四页）」，并补三项：

```yaml
  pages: [四页各自的版式、时长、对应口播句；每页出几个元素]
  differ-from: [和已上传视频拉开的是哪几项：分屏几何 / 底色明暗 / 中段版式 / 人物裁切 / 价格页构图]
  compliance: [本条涉及的审核硬规则和 local/ 里的禁用词，逐条写明怎么守]
```

风格先看 `references/styles/INDEX.md`，只读选中的 1～2 个文件；手法翻 `references/craft.md`。

### 第 3 步：骨架关键帧 + 相似度预检（停下来等用户）

用 `sh scripts/scaffold.sh <slug> --audio none` 建项目（或在使用者自己的出片管线里做），先用占位素材做出四页各一张关键帧（钩子页、步骤页、卖点墙、价格页），`node scripts/render.mjs <slug> --still <四个时刻> --sheet`。

拿这四张图做相似度预检（见上一节）。有像的先改版式再给用户看。把关键帧、预检结果、brief 摘要一起发给用户确认方向。**这一步之前不调用任何付费接口。**

### 第 4～5 步：配音、数字人

按上面「配音」「数字人片段」两节做。每一个 🛑 都要真的等用户回复。

### 第 6 步：制作

制作前读 `references/stack.md`（页面契约、确定性）。要现成写法时查 `references/recipes.md`。

- 口播时间轴先锁定（`references/narration.md`），再安排画面；换页时刻比该段口播早约 4 帧。
- 时间点全部写进 `timeline.js`；四页写进 `SHOTS`，刻意停留（价格页定格）写进 `HOLDS`。
- 画面只由 t 决定：不用 `Math.random`、`Date.now`、rAF、定时器、CSS 动画；字体自托管，加载完再 `READY = true`；布局从 `stageSize()` 推导。
- 每页渲开头、中段、结尾 3 张静帧；关键动作用 `inspect.mjs strip` 看连续帧。
- `render.mjs <slug> --determinism` 不通过就先修。
- 声音：换页 whoosh、每出一个元素 pop、价格 ding，BGM 压低（有口播时人声优先），见 `references/sound.md`。

### 第 7 步：预览

读 `references/editor.md`，运行 `node scripts/editor.mjs <slug> --size 1080x1920 --fps 30` 并主动打开。用户点「导出视频」或明确说可以导出，才进入下一步。

### 第 8 步：导出与验收

1. 技术检查（程序判定，FAIL 就不能交付）：
   ```bash
   node scripts/inspect.mjs qa <slug>/out/final.mp4 --out <slug>/qa/final \
     --expect-size 1080x1920 --expect-fps 30 --expect-duration <秒> --audio required
   ```
2. 审核硬规则自查：逐条对照上面九条和 `local/` 的禁用词，抽帧看每一页的文字。
3. 相似度终检：整条和所有已上传视频、同批其他条比，结果写进 `qa/review_log.md`。
4. 审片：按 `references/review.md` 的审片表写观察和最严重的 3 个问题；看 `inspect.mjs phone` 的手机尺寸图。审片不能代替用户自己看片。

### 第 9 步：交付

告诉用户：成片路径、封面（`render.mjs <slug> --poster <t>`）、brief、qa 结果（全部 PASS）、相似度结果、没解决的问题、第三方素材来源和授权。成片放到 `local/` 规定的待审批位置，**不直接发布、不操作广告账户**。

## 工具速查（`S=<skill>/scripts`）

| 目的 | 命令 |
|---|---|
| 装依赖 / 查环境 / 自测 | `cd $S && npm install && npx playwright install chromium` · `node $S/check-env.mjs` · `cd $S && npm test` |
| 拆参考片 | `node $S/inspect.mjs sheet <v> --cells 30` · `grid <v> --strips` · `heat <v>` |
| 成片验收 | `node $S/inspect.mjs qa <v> --expect-size 1080x1920 --expect-fps 30 --expect-duration <秒> --audio required` · `phone` · `strip --at <秒>` · `motion` |
| 建项目 | `sh $S/scaffold.sh <slug> [--audio synth\|tone\|layer\|file\|none]` |
| 静帧 / 封面 / 三个方向 | `node $S/render.mjs <slug> --still 0.5,6,15,24 --sheet` · `--poster <t>` · `--directions a,b,c --at …` |
| 确定性 | `node $S/render.mjs <slug> --determinism` |
| 声音 | `node $S/audio.mjs build <slug>/score.mjs` · `check <wav>` · `beats <track>` |
| 口播混音 | `node $S/narration.mjs import … · mix … · check …`（见 narration.md） |
| 预览 | `node $S/editor.mjs <slug> --size 1080x1920 --fps 30` |

## 参考文件（按需读）

| 文件 | 什么时候读 |
|---|---|
| `local/`（若有） | **开工前全部读** |
| `references/feed-ad.md` | 第 2、3 步：四页七句槽位、时长比例、版式要点、相似度预检方法 |
| `references/formats.md` | 只读 H 类（人物 + 代码场景） |
| `references/styles/INDEX.md` → 选中的 1～2 个风格文件 | 第 2 步选风格、裂变换风格 |
| `references/craft.md` | 节奏、运动、转场、排版、可读性 |
| `references/brief-template.md` | 写 brief |
| `references/stack.md`、`references/recipes.md` | 第 6 步制作 |
| `references/sound.md` | BGM、音效、混音 |
| `references/narration.md` | 配音导入、时间戳、混音 |
| `references/editor.md`、`references/progress.md` | 预览工作区、按需展示制作过程 |
| `references/review.md` | 第 8 步审片 |
| `references/long-form.md` | 只在做超过 2 分钟的讲解片时 |
