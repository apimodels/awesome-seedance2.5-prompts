# Handheld DV morning dog-walk vlog

- **Category:** Candid & Handheld
- **Clip:** 15s · 16:9
- **Prompt:** published by the author, quoted in full below, word for word. It belongs to its author; open an issue to have it removed.
- **Source:** [@maxxmalist](https://x.com/maxxmalist/status/2085422370362110168) — video by its author, linked for reference
- **In the gallery:** https://apimodels.app/seedance-2-5-prompts#prompt-cf387801f8c35408450aff56f

[![Handheld DV morning dog-walk vlog](https://pbs.twimg.com/amplify_video_thumb/2085417535650820096/img/aZuUimW67xW4-upN.jpg)](https://apimodels.app/seedance-2-5-prompts#prompt-cf387801f8c35408450aff56f)

## Why this one is worth reading

Built from six labelled blocks — CAMERA, LOOK, STYLE, CHARACTER, SETTING, SCENES — instead of one paragraph. Note that the flaws are specified on purpose: autofocus hunting, exposure breathing, brief accidental face cropping. Asking for imperfection is what separates "vlog" from "commercial".

## Prompt (full text, as posted)

````text
CAMERA: Handheld DV 16mm daily vlog footage. The video MUST begin with her holding the camera at arm's length in selfie mode while stepping outside her apartment building with her dog. The first 20–30 seconds are entirely handheld. Later she occasionally places the camera on a park bench, low stone wall, picnic table, or the ground for wider shots. Keep subtle handheld shake, drifting composition, autofocus hunting, rushed reframing, uneven zooms, exposure breathing, brief accidental face cropping, and imperfect framing throughout. The camera itself is never visible.

LOOK: Warm analog tape texture with gentle film grain, slightly softened sharpness, subtle halation around sunlight, realistic skin tones, low contrast, tiny exposure shifts, and natural motion blur. It should feel like authentic footage from someone's everyday life rather than a polished commercial.

STYLE: A relaxed morning lifestyle vlog. Quiet, cozy, and spontaneous. She occasionally laughs at her dog, pauses to look around, adjusts the leash, brushes hair away from her face, and speaks naturally in short sentences with comfortable pauses.

CHARACTER: EMMA — a beautiful white woman in her mid-20s. Long light brown hair in a messy ponytail, green eyes, minimal makeup, oversized gray hoodie, black biker shorts, white sneakers, and a small crossbody bag. She is walking a happy golden retriever.

SETTING: A peaceful suburban neighborhood on a sunny morning. Tree-lined sidewalks, quiet residential streets, birds singing, a small park with benches, green grass, and soft golden morning light. Very few people are around.

SCENES:

The vlog opens in selfie mode. Emma holds the camera while leaving her apartment building with the golden retriever excitedly pulling on the leash.
"Good morning."
She smiles.
"Someone couldn't wait."
The dog eagerly sniffs everything as they walk down the sidewalk.
She laughs quietly.
"He has to inspect every single tree."
Still holding the camera, she walks into a small neighborhood park.
The dog suddenly stops and stares at a squirrel.
"Oh... there we go."
She smiles and gently shakes her head.
She places the camera on a nearby bench for a wider angle while throwing a tennis ball.
The dog happily chases after it.
"Worth waking up early."
She picks the camera back up.
Walking slowly through the park, she looks up at the trees for a moment.
"It's actually really peaceful out here."
The dog returns with the ball but drops it halfway.
She laughs.
"Close enough."
She sits on the bench while the dog lies beside her.
She scratches behind his ears.
"I think he's happier than I am."
She stands up and continues walking.
The camera stays in selfie mode as they head toward home.
"Coffee is definitely next."
She smiles into the lens.
"See you later."
She gives a small wave and ends the recording.
````

Also in the full library as [SD002](../library/documentary/SD002.md).

**Run it** — Seedance 2.5 is live on apimodels.app as `seedance-2.5`: $0.120/s at 480p, $0.270/s at 720p, billed on real token usage and charged only on success.

```bash
curl -X POST https://apimodels.app/api/v1/video/generations \
  -H "Authorization: Bearer $APIMODELS_API_KEY" -H "Content-Type: application/json" \
  -d '{"model":"seedance-2.5","prompt":"<the full prompt above>","duration":15,"resolution":"480p"}'
```

The clip is 15 s ($1.80 at 480p, $4.05 at 720p) even though the prompt talks about "the first 20–30 seconds" — length is decided by `duration`, not by the text, and it is also what moves the bill (4–30 s in one pass, or `-1` to let the model choose). The API exposes 480p and 720p only. [Docs](https://apimodels.app/docs/seedance-2-5) · [model](https://apimodels.app/models/seedance-2.5)

---

这条的中文说明:不是一整段，而是 CAMERA / LOOK / STYLE / CHARACTER / SETTING / SCENES 六个带标签的块。注意它是**刻意要缺陷**的：自动对焦来回拉、曝光呼吸、偶尔把脸切掉一半。主动要求不完美，才是 vlog 和广告片的分界线。

**用 API 跑这条** — `seedance-2.5` 已在 apimodels.app 上线，命令同上（prompt 换成上面的全文）：480p $0.120/秒、720p $0.270/秒，按真实用量计费，只在成功时扣费。

成片是 15 秒（480p 约 $1.80，720p 约 $4.05），尽管提示词里写着「前 20—30 秒」——片长由 `duration` 决定，不由文字决定，它同时也是账单的开关（单次 4–30 秒，或填 `-1` 让模型自己定）。API 只开放 480p 和 720p。文档：[/docs/seedance-2-5](https://apimodels.app/docs/seedance-2-5)
