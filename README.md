# Awesome Seedance 2.5 Prompts

[![Gallery](https://img.shields.io/badge/Browse%209%20prompts%20with%20video-F5FF60?labelColor=111)](https://apimodels.app/seedance-2-5-prompts)
[![One API](https://img.shields.io/badge/One%20API-85%2B%20models-3158E8)](https://apimodels.app/models)
[![Seedance 2.5](https://img.shields.io/badge/Seedance%202.5%20live-from%20%240.134%2Fs-1f9e5f)](https://apimodels.app/models/seedance-2.5)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

A curated library of **Seedance 2.5 video prompts** — every one shown next to the clip it
actually produced, with credit and a link to the creator's original post.

**[中文说明](./README.zh-CN.md)** · **[Browse all 9 prompts](./prompts/GALLERY.md)** ·
**[Watch them with sound](https://apimodels.app/seedance-2-5-prompts)** ·
**[Jump to the prompting guide](#seedance-25-prompts-guide)**

---

## What Seedance 2.5 does

ByteDance unveiled Seedance 2.5 on **23 June 2026** at its Volcano Engine FORCE conference.
By ByteDance's announced figures:

| | Seedance 2.5 | Seedance 2.0 (for comparison) |
|---|---|---|
| Length in one pass | **30 s** | 4–15 s |
| Resolution | **480p / 720p** on the API (the announced native 4K 10-bit is not exposed) | up to 1080p on the official channel |
| Reference assets per job | **up to 50** | up to 9 images + video + audio |
| — images | up to 30, each ≤ 4K | 9 |
| — video / audio | up to 10 clips each, 30 s total each | 1 video + 1 audio |
| Editing | localised scene editing — swap a product or background without re-rolling | — |
| Audio | generated in the same latent space as the picture | native synced audio |

ByteDance also shipped an **official prompting manual** for it, written by the people who
trained the model. We walked through it in English here:
**[The Seedance 2.5 Prompting Guide](https://apimodels.app/blog/seedance-2-5-prompting-guide)**.

> **Sourcing.** The numbers above are ByteDance's published figures, not our measurements —
> we do not have API access to 2.5 yet (see [Where to run these](#where-to-run-these-prompts)),
> so we are not going to present announced specs as tested ones.

---

## Seedance 2.5 prompts guide

Everything below comes from three places, kept separate on purpose: ByteDance's official
manual, the nine prompts in this library, and field notes from a creator who spent roughly
50,000 credits (about ¥50,000) testing 2.5 on Dreamina.

### The order that works

Write the parts in this order rather than describing a mood:

```
subject → action → location → camera work → lighting → picture texture → sound
```

Only the first two are required; drop anything you do not need. "A person walking" gets you
a stock loop. The same subject with a camera move and a light direction attached gets you a
shot:

> A person slowly walks through a city at dusk. The camera follows from behind, then swings
> around to a side profile midway. Soft backlighting, cinematic colour tones, natural
> movement of clothing and hair.

The official base template:

```
TEMPLATE

<SUBJECT> <main action or event> in <scene and environment>.
The image is <visual style>.
The camera uses <shot size, position, movement or cutting>.
Sound includes <dialogue, ambience, effects or music>.
```

### Thirty seconds is written as stages, not as longer sentences

This is the single biggest difference from 10-second models. Padding a short prompt with
adjectives does not produce 30 good seconds; splitting the event into staged states does.
Each stage gets **one** main event and an **end state that the next stage inherits**:

```
TEMPLATE — long video

[GOAL]
Generate a <video type>. The core subject is <subject>; the main event is <story summary>.

[STAGE ONE]
Opens with:   <initial state of people, props and scene>.
Main event:   <one main action or event>.
Ends with:    <person position, prop ownership or picture state>.

[STAGE TWO]
Carried over: <state that must be preserved>.
Main event:   <one main action or event>.
Ends with:    <observable state>.

[STAGE THREE]
Main event:   <closing event>.
Ends with:    <final picture state>.

[KEEP CONSISTENT]
Keep <identity, headcount, clothing, prop ownership, spatial orientation
and sound relationships> stable.
```

Plain timed ranges work too — `0–5s`, `5–10s` — and several prompts here use them. The rule
is the same either way: **one main movement per segment**. Cram three actions into five
seconds and all three get compressed into mush.

And describe each action **exactly once**. The official guide is blunt about this: repeating
the same action in different words degrades it rather than reinforcing it.

### Give every reference asset a job *and* an exclusion

Not "here are my images" but a role and a boundary:

```
TEMPLATE — asset roles

@image1 supplies <subject>'s <appearance, clothing, structure or material>.
        Do not take <the background / the pose / the other people>.
@video1 supplies <action, camera movement or rhythm>.
@audio1 supplies <character or sound type>'s <timbre, dialogue, ambience or music>.
```

You can attach up to 50 assets. The guide's recommended ranges are much narrower — 1–8
image subjects, 1–5 video subjects at 5–10 s each — and it states the trade-off plainly:
**the more assets you attach, the more easily stability drops**. Assign roles or pay for it.

### Six habits that separate the good prompts here from the rest

1. **Name your subjects and reuse the name.** Write `<SOLDIER>`, `<SHARI>`, `<WOMAN>` once
   and refer to that token every time after. Over 30 seconds, "she" and "the man" drift onto
   the wrong body. A named token is the cheapest identity lock there is.
2. **Write the sound as a cue sheet, not a mood.** Audio comes out of the same pass as the
   picture. List the ambience, the specific foley, dialogue with the language named, and
   what should be absent. [One prompt here](./prompts/dialogue/seven-shot-bedroom-candid-cat-call-doorbell.md)
   ends with a full foley list, and it is a large part of why the clip looks finished.
3. **Ask for the imperfections you want.** Handheld shake, autofocus that settles half a
   beat late, exposure breathing, framing that clips a face. Realism here is a list of
   specified flaws — leave them out and you get a clean commercial no matter how many times
   you write "candid".
4. **Freeze means freeze.** Models drift. If something must be motionless, say
   *no drift, no wobble, no micro-motion* — worth more than any adjective about time stopping.
5. **Close with a negative list.** No subtitles, no watermark, no extra limbs, no identity
   swap. For reference-driven jobs add the one people forget:
   *never render a reference sheet or duplicate the subject.*
6. **Keep generation parameters out of the prompt.** Resolution, duration and aspect ratio
   are set on the generation page or through the API, not in the text.

### Field notes from 50,000 credits of testing

A creator who ran ~¥50,000 of credits through Seedance 2.5 on Dreamina reports, in addition
to the above: extension can push a clip to roughly **3 minutes** beyond the 30-second native
length, timestamps can be addressed with **sub-second precision**, consistency holds up well
in long cinematic takes, and post-generation editing is materially better than the previous
generation. Treat these as one practitioner's experience rather than published specification —
they are consistent with what the official guide describes, but we have not measured them.

---

## Two kinds of prompt, kept clearly apart

| | Count | What it is |
|---|---|---|
| **Author-written** | 3 | Published by the creator. Credited and linked to the original post. Full text lives in our [gallery](https://apimodels.app/seedance-2-5-prompts) — we index it here rather than copy it, because we do not own it. |
| **Reconstructed** | 6 | For clips whose creator never published a prompt, we sample frames from the finished video and write the prompt that would most plausibly reproduce it. **MIT, full text in this repo.** |

A reconstruction describes the *output*. It cannot recover negative constraints, exact
dialogue or reference-image workflows — it is a writing reference, not the creator's prompt,
and every one is labelled `reconstructed`.

**Languages.** Prompts are stored in the language their author wrote them in — we do not
translate them, because a translated prompt does not generate the same clip. Our own
reconstructions are written natively in both English and Chinese.

**Where the clips ran.** The creators here used ByteDance's own Dreamina (Jimeng) and
Higgsfield. Where a post named the platform, the entry says so.

Creators: if you would like an entry removed or a credit corrected, open an issue.

---

## The prompts

**[Browse all 9 with preview stills →](./prompts/GALLERY.md)**

| # | Prompt | Category | Length | Source |
|---|---|---|---|---|
| 1 | [Seven-shot bedroom candid — cat, phone call, doorbell](./prompts/dialogue/seven-shot-bedroom-candid-cat-call-doorbell.md) | Dialogue & Lip Sync | 15 s | [@oggii_0](https://x.com/oggii_0/status/2085640281941307648) · author's own |
| 2 | [Handheld DV morning dog-walk vlog](./prompts/documentary/handheld-dv-morning-dog-walk-vlog.md) | Candid & Handheld | 15 s | [@maxxmalist](https://x.com/maxxmalist/status/2085422370362110168) · author's own |
| 3 | [Hand-to-hand combat in a rain-flooded metro hall](./prompts/action/rain-flooded-metro-station-hand-to-hand-fight.md) | Action & Fight | 30 s | [@lansenai](https://x.com/lansenai/status/2083521805176988016) · author's own |
| 4 | [The rice that rode the belt looking for its topping](./prompts/product/conveyor-sushi-rice-finds-its-match.md) | Product & Ads | 30 s | [@hahazwei](https://x.com/hahazwei/status/2085219893180563470) · reconstructed |
| 5 | [Red-hooded armoured soldier in desert ruins](./prompts/reference/red-hooded-mech-soldier-in-desert-ruins.md) | Reference & Consistency | 30 s | [@LudovicCreator](https://x.com/LudovicCreator/status/2084217894926258534) · reconstructed |
| 6 | [Silhouette transformation in a lightning void](./prompts/cinematic/lightning-sorceress-transformation.md) | Cinematic & VFX | 30 s | [@LudovicCreator](https://x.com/LudovicCreator/status/2083976170932989982) · reconstructed |
| 7 | [Building breakfast inside a frozen diner](./prompts/cinematic/frozen-diner-breakfast-heist.md) | Cinematic & VFX | 30 s | [@techhalla](https://x.com/techhalla/status/2085313653662707968) · reconstructed |
| 8 | [The cat that has changed pose every time she walks past](./prompts/animation/the-cat-that-changes-pose-every-time.md) | Animation & Anime | 20 s | [@pan_soramame_da](https://x.com/pan_soramame_da/status/2085493871639994803) · reconstructed |
| 9 | [Thirty-second selfie day-in-the-life](./prompts/long-form/thirty-second-selfie-day-in-the-life.md) | 30 s & Multi-Shot | 30 s | [@onofumi_AI](https://x.com/onofumi_AI/status/2083560874443432048) · reconstructed |

The longest prompt in the library is **4,576 characters** — a 30-second fight scene with two
identities locked from reference images, a fixed floor plan the camera may not contradict,
five timed beats, and a closing block of negative constraints. It is the clearest single
demonstration of what 30 seconds costs you in writing.

---

## Where to run these prompts

**Seedance 2.5 is live on apimodels.app** as the model `seedance-2.5`, from **$0.134/s**
at 480p and $0.300/s at 720p — one API key, no Volcengine account and no enterprise
verification. It generates 4-30 seconds in a single pass, takes up to 50 reference assets
(30 images + 10 videos + 10 audios), and adds video editing and video extension.

Two things the launch coverage gets wrong, so they are worth stating plainly:

- **The API is 480p and 720p only.** The "native 4K, 10-bit" figure above is what ByteDance
  announced at FORCE; it is not a resolution the API exposes. If you need 1080p or 4K today,
  use [Seedance 2.0](https://apimodels.app/models/seedance-2.0).
- **Reference-video jobs are not cheaper.** Editing or extending a clip bills on
  (source seconds + output seconds), so turning a clip into an output of the same length
  costs about 20-25% more than generating that length outright.

Docs: **[/docs/seedance-2-5](https://apimodels.app/docs/seedance-2-5)**

Today, the creators in this library run 2.5 in **Dreamina (Jimeng)** and **Higgsfield**.

What you *can* call through us right now, with the same key and the same endpoint — so
migrating to 2.5 when it opens is a one-string change:

| Model | From | What it is |
|---|---|---|
| **[Seedance 2.0](https://apimodels.app/models/seedance-2.0)** | **$0.092** / s | ByteDance official Ark: 9 reference images + reference video + audio, native synced audio |
| [Seedance 2.0 Fast](https://apimodels.app/models/seedance-2.0-fast) | **$0.071** / s | Same capability, speed/cost tier |
| [Seedance 2.0 Mini](https://apimodels.app/models/seedance-2.0-mini) | **$0.044** / s | Cheapest Seedance tier |
| [Dreamina Seedance 2.0](https://apimodels.app/models/dreamina-seedance-2-0) | per second | International line, native up to 4K 10-bit |
| **[MiniMax H3](https://apimodels.app/models/minimax-h3)** | **$0.145** / s | Native 2K + synced audio, 9 ref images + 3 videos + 3 audio |
| **[Kling V3](https://apimodels.app/models/kling-v3)** | **$0.12** / s | 3–15 s, text- and image-to-video, optional audio |
| [VEO 3.1](https://apimodels.app/models/veo-3.1) | per clip | Premium standard tier |

Pay as you go, no subscription, **$1 free on sign-up**, and only successful requests are
charged. Full list: **[apimodels.app/models](https://apimodels.app/models)** ·
API docs: **[apimodels.app/docs/video](https://apimodels.app/docs/video)**

### 30-second start

One endpoint, one key; the model name is the only thing that changes between models:

```bash
curl -X POST https://apimodels.app/api/v1/video/generations \
  -H "Authorization: Bearer $APIMODELS_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model":"seedance-2.0","prompt":"A luthier lifts a finished violin off the bench and sets it upright in the drying rack. Late afternoon light rakes through sawdust. The camera pushes slowly in on the grain of the top plate.","duration":5,"resolution":"480p"}'
```

---

## Related libraries

- **[Stunning MiniMax H3 Prompts](https://github.com/stimQQ/stunning-minimax-h3-prompts)** —
  222 MiniMax H3 (Hailuo 3) video prompts, same format.
- **[GPT Image 2 Prompts](https://github.com/stimQQ/gpt-image-2-prompts)** — 955 image
  prompts with the image each one rendered.

## Contributing

Open an issue with the link to the original post and, if the creator published it, the prompt
text. Two things we check before merging: the prompt is attributable to a real post, and the
clip is actually Seedance 2.5 rather than another model.

## License

Everything we wrote — the reconstructed prompts, the guide, the indexes — is
[MIT](./LICENSE). Author-written prompts belong to their authors and are indexed here with
credit, not relicensed. Preview stills are single frames from the creators' own posts,
included for identification and linked back to the source.
