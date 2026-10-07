# Awesome Seedance 2.5 Prompts · Seedance 2.5 提示词库

[![画廊](https://img.shields.io/badge/95%2B%20条提示词%20·%20带成片-F5FF60?labelColor=111)](https://apimodels.app/zh/seedance-2-5-prompts)
[![一个 API](https://img.shields.io/badge/一个%20API-85%2B%20模型-3158E8)](https://apimodels.app/zh/models)
[![Seedance 2.5](https://img.shields.io/badge/Seedance%202.5%20已上线-%240.134%2F秒起-1f9e5f)](https://apimodels.app/zh/models/seedance-2.5)
[![参考图](https://img.shields.io/badge/参考图-%240.008%2F张起-8b5cf6)](#参考图总得先有)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

精选 **Seedance 2.5 视频提示词**——每条都配上它真实生成的那段成片，署名作者并链回原帖。

**[English](./README.md)** · **[看全部 9 条](./prompts/GALLERY.zh-CN.md)** ·
**[在画廊里带声音看](https://apimodels.app/zh/seedance-2-5-prompts)** ·
**[直接跳到写法指南](#seedance-25-提示词写法指南)**

---

## Seedance 2.5 是什么

字节跳动 **2026 年 6 月 23 日**在火山引擎 FORCE 大会发布 Seedance 2.5。按官方公布的数字：

| | Seedance 2.5 | Seedance 2.0（对照） |
|---|---|---|
| 单次生成时长 | **30 秒** | 4–15 秒 |
| 分辨率 | API 上是 **480p / 720p**（公布的原生 4K 10-bit 并未开放） | 官方渠道上限 1080p |
| 单次参考素材 | **最多 50 份** | 最多 9 张图 + 参考视频 + 参考音频 |
| — 图片 | 最多 30 张，单张 ≤ 4K | 9 张 |
| — 视频 / 音频 | 各最多 10 段，各自总时长 ≤ 30 秒 | 各 1 段 |
| 编辑 | 局部编辑：换产品或背景不必重生成整条 | — |
| 音频 | 与画面在同一潜空间生成 | 原生同步音频 |

字节还为它发布了一份**官方提示词指南**，由训练这个模型的人写的。我们整理过完整的英文版：
**[Seedance 2.5 官方提示词指南](https://apimodels.app/zh/blog/seedance-2-5-prompting-guide)**。

> **关于出处。** 上表是字节公布的数字。我们自己在正式接口上跑过的部分会明确标成实测——
> 下面[在哪能跑](#在哪能跑这些提示词)里「只有 480p / 720p」和那两条计费口径，是我们
> 2026 年 8 月 8 日实测的结论。公布的规格和测过的规格，这里一直分开讲。

---

## Seedance 2.5 提示词写法指南

下面的内容来自三处，刻意分开标注：字节的官方指南、本库这 9 条提示词里真实出现过的写法，
以及一位在即梦（Dreamina）上烧掉约 5 万点（约 5 万日元）实测 2.5 的创作者的经验总结。

### 有效的顺序

按这个顺序逐项写，而不是描述一种氛围：

```
主体 → 动作 → 地点 → 运镜 → 光线 → 画面质感 → 声音
```

只有前两项是必须的，其余按需取用。「一个人在走路」只会给你一段素材库循环；同一个主体，
加上镜头怎么动、光从哪来，才是一个镜头：

> 一个人在黄昏的城市里缓步而行。镜头先从背后跟随，中途摇转到侧脸。柔和的逆光，
> 电影感的色调，衣物和头发自然摆动。

官方的基础模板：

```
基础模板

<主体>在<场景与环境>中<主要动作或事件>。
画面呈现<视觉风格>。
镜头采用<景别、机位、运镜或切镜>。
声音包括<对白、环境声、音效或音乐>。
```

### 30 秒是「分阶段」写出来的，不是把句子写长

这是和 10 秒级模型最大的差别。把短提示词堆满形容词，并不会变出 30 秒好内容；
把事件拆成层层继承的状态才会。每个阶段给**一个**主线事件，和一个**下一阶段要继承的结束状态**：

```
长视频模板

【目标】
生成一段<视频类型>。核心主体是<主体>；主线事件是<故事概要>。

【第一阶段】
开场状态：<人物、道具与场景的初始状态>。
主线事件：<一个主要动作或事件>。
结束状态：<人物位置、道具归属或画面状态>。

【第二阶段】
承接状态：<必须保持不变的状态>。
主线事件：<一个主要动作或事件>。
结束状态：<可观察到的状态>。

【第三阶段】
主线事件：<收尾事件>。
结束状态：<最终画面状态>。

【保持一致】
保持<身份、人数、服装、道具归属、空间朝向与声音关系>稳定。
```

直接写时间段也行——`0—5 秒`、`5—10 秒`，本库里好几条就是这么写的。无论哪种写法，
规则一样：**一个时间段只放一个主要动作**。五秒里塞三个动作，三个都会被压成一团糊。

而且每个动作**只描述一次**。官方指南说得很直白：把同一个动作换种说法写第二遍，
不是加强，而是劣化。

### 每份参考素材都要给职责，也要给排除项

不要只说「这是我的图」，要给角色和边界：

```
素材职责模板

@图1 提供<主体>的<外观、服装、结构或材质>。
      不要采用<背景 / 姿势 / 画面里的其他人>。
@视频1 提供<动作、镜头运动或节奏>。
@音频1 提供<角色或声音类型>的<音色、台词、环境声或音乐>。
```

单次最多可挂 50 份素材。但官方的**推荐范围窄得多**——主体图 1 至 8 个主体，
主体音视频 1 至 5 个、单段 5 至 10 秒——而且把代价写得很直白：
**素材越多，稳定性越容易下降**。要么指派职责，要么为此付出代价。

### 六条把好提示词和普通提示词分开的习惯

1. **给主体起名字，然后一直用这个名字。** 先写一次 `<士兵>`、`<醋饭>`、`<女生>`，
   之后每次都用这个标记。30 秒里，「她」和「那个男人」会漂到错误的身体上——
   命名标记是成本最低的身份锁。
2. **声音要写成音效清单，不是写气氛。** 音频和画面是同一次生成出来的。直接列环境声、
   具体的拟音、注明语种的对白，以及不要出现什么。[本库有一条](./prompts/dialogue/seven-shot-bedroom-candid-cat-call-doorbell.md)
   结尾就是一整份拟音清单，这正是它「完成度高」的一大半原因。
3. **主动要求你想要的缺陷。** 手持抖动、慢半拍才合上的自动对焦、曝光呼吸、把脸切掉一半的构图。
   这个模型里的真实感就是一份写明的缺陷清单——不写，你写多少遍「纪实」都还是干净的广告片。
4. **定格就要真的不动。** 模型会漂。如果某样东西必须静止，就直说
   *不漂移、不晃动、没有任何微动*——比任何「时间静止」的形容词都管用。
5. **结尾放负向清单。** 不要字幕、不要水印、不要多出手脚、不要身份互换。用参考图时
   还要加上大家最常忘的那句：*永远不要把参考拼图本身画出来，也不要复制主体。*
6. **参数不要写进提示词。** 分辨率、时长、画幅是在生成页面或接口里设置的，不是正文内容。

### 来自 5 万点实测的经验

一位在即梦上跑掉约 5 万点（约 5 万日元）的创作者，除以上之外还报告：
在 30 秒原生时长之外，用**延长**可以把片子推到约 **3 分钟**；时间戳可以精确到**亚秒级**；
电影感长镜头下的一致性表现良好；生成后的编辑功能相比上一代有实质提升。
这些是一位实践者的经验，不是公布的规格——它们和官方指南的描述一致，但我们没有实测过。

---

## 两类提示词，明确分开

| | 数量 | 是什么 |
|---|---|---|
| **作者原文** | 3 条 | 作者自己公开的。带署名、链回原帖。全文放在我们的[画廊页](https://apimodels.app/zh/seedance-2-5-prompts)，本仓库只做索引不复制——因为版权不归我们。 |
| **反推** | 6 条 | 作者从未公开提示词的成片，我们从成片抽帧，写出最可能复现它的那条提示词。**MIT，全文在本仓库。** |

反推描述的是**结果**。它拿不到负向约束、精确台词和参考图工作流——它是写法参考，
不是作者的原始提示词，每一条都标了 `reconstructed`。

**语言。** 提示词按作者原本书写的语言保存，我们**不翻译**——翻译过的提示词跑出来
不是同一段片子。我们自己的反推稿则是中英各写一遍，不逐句互译。

**成片在哪跑的。** 本库作者分别用了字节自家的即梦（Dreamina）和 Higgsfield。
原帖里注明了平台的，条目上会写。

作者们：如果希望撤下某条或更正署名，提个 issue 即可。

---

## 全部提示词

**[带预览图浏览全部 9 条 →](./prompts/GALLERY.zh-CN.md)**

| # | 提示词 | 分类 | 时长 | 出处 |
|---|---|---|---|---|
| 1 | [七镜卧室纪实——猫、来电、门铃](./prompts/dialogue/seven-shot-bedroom-candid-cat-call-doorbell.md) | 对白与口型 | 15 秒 | [@oggii_0](https://x.com/oggii_0/status/2085640281941307648) · 作者原文 |
| 2 | [手持 DV 清晨遛狗 vlog](./prompts/documentary/handheld-dv-morning-dog-walk-vlog.md) | 纪实与手持真实感 | 15 秒 | [@maxxmalist](https://x.com/maxxmalist/status/2085422370362110168) · 作者原文 |
| 3 | [暴雨地铁检修站·30 秒现代格斗](./prompts/action/rain-flooded-metro-station-hand-to-hand-fight.md) | 动作与格斗 | 30 秒 | [@lansenai](https://x.com/lansenai/status/2083521805176988016) · 作者原文 |
| 4 | [在回转带上找配对的醋饭](./prompts/product/conveyor-sushi-rice-finds-its-match.md) | 产品与广告 | 30 秒 | [@hahazwei](https://x.com/hahazwei/status/2085219893180563470) · 反推 |
| 5 | [走出沙漠废墟的红帽装甲兵](./prompts/reference/red-hooded-mech-soldier-in-desert-ruins.md) | 参考素材与一致性 | 30 秒 | [@LudovicCreator](https://x.com/LudovicCreator/status/2084217894926258534) · 反推 |
| 6 | [雷电虚空中的剪影变身](./prompts/cinematic/lightning-sorceress-transformation.md) | 电影感与特效 | 30 秒 | [@LudovicCreator](https://x.com/LudovicCreator/status/2083976170932989982) · 反推 |
| 7 | [在被定格的餐车里现做早餐](./prompts/cinematic/frozen-diner-breakfast-heist.md) | 电影感与特效 | 30 秒 | [@techhalla](https://x.com/techhalla/status/2085313653662707968) · 反推 |
| 8 | [每次路过都换个睡姿的猫](./prompts/animation/the-cat-that-changes-pose-every-time.md) | 动画与二次元 | 20 秒 | [@pan_soramame_da](https://x.com/pan_soramame_da/status/2085493871639994803) · 反推 |
| 9 | [30 秒自拍式一日 vlog](./prompts/long-form/thirty-second-selfie-day-in-the-life.md) | 30 秒长片与分阶段 | 30 秒 | [@onofumi_AI](https://x.com/onofumi_AI/status/2083560874443432048) · 反推 |

本库最长的一条是 **4576 字**：30 秒格斗戏，两个用参考图锁死的身份、一张镜头不得自相矛盾的
平面图、五个计时段落，外加结尾一整块负向约束。它最能说明「30 秒」在写作上要付出什么。

---

## 在哪能跑这些提示词

**Seedance 2.5 已在 apimodels.app 上线**，模型名 `seedance-2.5`，480p **$0.134/秒**起、
720p $0.300/秒——一个 API Key 即可，无需火山账号、无需企业认证。单次出片 4–30 秒，
一个任务最多 50 份参考素材（30 图 + 10 视频 + 10 音频），并新增视频编辑与视频续写。

有两点各家报道容易搞错，这里直说：

- **API 上只有 480p 和 720p。** 上面表格里那个「原生 4K、10-bit」是字节在 FORCE 发布会
  公布的口径，API 并没有暴露这一档。今天要 1080p 或 4K，请用
  [Seedance 2.0](https://apimodels.app/zh/models/seedance-2.0)。
- **带参考视频不等于更便宜。** 编辑或续写按「源片秒数 + 输出秒数」计费，所以把一段素材
  改成等长的成片，比直接生成同样长度贵约 20–25%。

文档：**[/docs/seedance-2-5](https://apimodels.app/zh/docs/seedance-2-5)**

今天，本库这些作者是在**即梦（Dreamina）**和 **Higgsfield** 上跑的 2.5。

同一个端点、同一把 key 还能调的其它视频模型（换模型只改 model 这一个字符串）：

| 模型 | 起价 | 是什么 |
|---|---|---|
| **[Seedance 2.0](https://apimodels.app/zh/models/seedance-2.0)** | **$0.092** / 秒 | 火山方舟官方直连：9 张参考图 + 参考视频 + 参考音频，原生同步音频 |
| [Seedance 2.0 Fast](https://apimodels.app/zh/models/seedance-2.0-fast) | **$0.071** / 秒 | 能力相同的速度/成本档 |
| [Seedance 2.0 Mini](https://apimodels.app/zh/models/seedance-2.0-mini) | **$0.044** / 秒 | 最便宜的 Seedance 档位 |
| [Dreamina Seedance 2.0](https://apimodels.app/zh/models/dreamina-seedance-2-0) | 按秒 | 国际线，原生最高 4K |
| **[MiniMax H3](https://apimodels.app/zh/models/minimax-h3)** | **$0.145** / 秒 | 原生 2K + 同步音频，9 图 + 3 视频 + 3 音频 |
| **[Kling V3](https://apimodels.app/zh/models/kling-v3)** | **$0.12** / 秒 | 3–15 秒，文生/图生视频，可选音频 |
| [VEO 3.1](https://apimodels.app/zh/models/veo-3.1) | 按条 | 高端标准档 |

按量计费、无订阅、**注册送 $1**，且只对成功请求扣费。全部模型：
**[apimodels.app/models](https://apimodels.app/zh/models)** ·
接口文档：**[apimodels.app/docs/video](https://apimodels.app/zh/docs/video)**

### 参考图总得先有

Seedance 2.5 单个任务最多吃 **30 张参考图**，而本库大半的提示词都压在这上面：一套不能漂
的服装、一件必须自始至终是同一件的产品、一个镜头不许拍穿帮的场景。这些板子说到底就是图，
同一把 key、同一个域名就能生成。下面是每张图的价格，按原生 1K / 2K / 4K 分档——中间没有
任何放大器，且只有出图成功才扣费。

| 模型 | 调用名 | 1K | 2K | 4K |
|---|---|---|---|---|
| **[GPT Image 2](https://apimodels.app/zh/models/gpt-image-2)** | `gpt-image-2` | **$0.025** | $0.03 | $0.05 |
| [GPT Image 2 Lite](https://apimodels.app/zh/models/gpt-image-2-lite) | `gpt-image-2-lite` | **$0.008** | $0.015 | $0.025 |
| **[Nano Banana Pro](https://apimodels.app/zh/models/nanobananapro)**（Gemini 3 Pro Image） | `gemini-3-pro-image-preview` | **$0.06** | $0.06 | $0.12 |
| [Nano Banana 2](https://apimodels.app/zh/models/nanobanana2)（Gemini 3.1 Flash Image） | `gemini-3.1-flash-image-preview` | **$0.05** | $0.05 | $0.08 |

> **人脸是例外，这条最好在花钱之前就知道。**
> 火山对每一张直接传给 Seedance 的 `http(s)` 原图都会在**建任务的那一刻**过审，判定像真人
> 就直接拒。2026 年 8 月 8 日我们在 2.5 上又撞了一次——用的还是字节自己文档里的示例图当
> 首帧——任务在排队之前就被打回，所以不花钱，但也什么都没拿到。虚构的、非真实的人物正常
> 通过。要指定**某个真人**，先把这张人像注册进素材库，然后传它的 `asset://` id，而不是 URL。
>
> 也就是说：上面这几个图片模型负责**场景、产品、服装、道具和风格板**；人走 `asset://`。

接线之前还有一条值得先知道：**首帧与参考素材互斥。** `first_frame_url` / `last_frame_url`
不能和 `reference_image_urls` / `reference_video_urls` / `reference_audio_urls` 同时传，
两种输入方式只能选一种。同时传会被直接拒，而不是默默忽略掉其中一边（2026 年 8 月 8 日实测）。

```bash
# 1) 先做参考图。异步：返回 taskId，用同一个端点轮询拿结果 URL。
curl -X POST https://apimodels.app/api/v1/images/generations \
  -H "Authorization: Bearer $APIMODELS_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model":"gpt-image-2","resolution":"2K","aspect_ratio":"16:9",
       "prompt":"无缝深灰背景上的产品静物：一只哑光黑咖啡罐，拉丝钢盖，单一硬光从镜头左侧打来，标签上没有文字"}'

# 2) 把出好的图直接喂给视频任务——同一把 key、同一个域名。
#    在提示词里按顺序引用为 图片1 / @image1。
curl -X POST https://apimodels.app/api/v1/video/generations \
  -H "Authorization: Bearer $APIMODELS_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model":"seedance-2.5","duration":8,"resolution":"720p",
       "reference_image_urls":["<第 1 步拿到的结果 URL>"],
       "prompt":"图片1 里的咖啡罐居中摆放，硬光扫过罐盖。镜头缓慢推近；标签保持与 图片1 完全一致。"}'
```

### 30 秒上手

一个端点、一把 key，模型之间只改 model 这一个字符串：

```bash
curl -X POST https://apimodels.app/api/v1/video/generations \
  -H "Authorization: Bearer $APIMODELS_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model":"seedance-2.0","prompt":"制琴师把做好的小提琴从台钳上取下，立着放进阴干架。午后斜光穿过悬浮的木屑，镜头缓慢推近面板木纹。","duration":5,"resolution":"480p"}'
```

---

## 相关仓库

- **[Stunning MiniMax H3 Prompts](https://github.com/apimodels/stunning-minimax-h3-prompts)**
  —— 222 条 MiniMax H3（海螺 3）视频提示词，同样的格式。
- **[GPT Image 2 Prompts](https://github.com/apimodels/gpt-image-2-prompts)** —— 955 条图片
  提示词，每条都附它渲染出的图。

## 参与补充

提个 issue，带上原帖链接；作者公开过提示词的话，把原文一起贴上。合并前我们会核两件事：
这条能对应到一个真实存在的帖子，以及成片确实是 Seedance 2.5 而不是别的模型。

## 授权

我们写的部分——反推提示词、这份指南、各索引——采用 [MIT](./LICENSE)。作者原文版权归作者所有，
本仓库只带署名索引，不重新授权。

预览取自作者原帖，仅用于识别，每一条都链回出处：索引页是单帧静图，单条提示词页是一段
2.5 秒、400 像素宽、10 帧/秒的无声节选。成片本身的版权属于作者，本仓库不对其重新授权。
**如果你是其中某条的作者、不希望我们托管你成片的节选，开个 issue 即可，我们会立刻退回静图
或直接删掉——不争辩、不拖延。**
