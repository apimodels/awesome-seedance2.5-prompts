# Seven-shot bedroom candid — cat, phone call, doorbell

- **Category:** Dialogue & Lip Sync
- **Clip:** 15s · 16:9 · run on Higgsfield
- **Prompt:** published by the author, quoted in full below, word for word. It belongs to its author; open an issue to have it removed.
- **Source:** [@oggii_0](https://x.com/oggii_0/status/2085640281941307648) — video by its author, linked for reference
- **In the gallery:** https://apimodels.app/seedance-2-5-prompts#prompt-c50b543be1ee8d4b7e609bbc0

[![Seven-shot bedroom candid — cat, phone call, doorbell](https://pbs.twimg.com/amplify_video_thumb/2085640247682224128/img/Wj08brZzXojtfWtv.jpg)](https://apimodels.app/seedance-2-5-prompts#prompt-c50b543be1ee8d4b7e609bbc0)

## Why this one is worth reading

A 15-second clip cut into seven numbered shots with explicit second ranges, four Korean lines with lip sync, and a closing foley cue sheet. The last two sentences are the negative constraints — "no subtitles, no on-screen text, no logo, no watermark. Never render a reference sheet or duplicate the subject" — which is how you stop a reference-driven job from drawing the reference sheet itself.

## Prompt (full text, as posted)

````text
Montage, multi-shot candid observational footage. Do not use a single camera angle or continuous take. Handheld documentary style with the feeling of accidental real-life capture. Slightly imperfect framing, subtle handheld shake, tiny reframing adjustments, gentle exposure breathing, and autofocus that settles half a beat late. Realistic skin texture, soft indoor natural light, film grain, shallow depth of field. Relaxed breathing, natural blinking, restrained and authentic performance. Total of 7 shots.
The woman from @ Image 1 is wearing a matching cotton pajama set consisting of a scoop-neck sleeveless top and loose shorts made from the same fabric and design. Barefoot, she lies on her stomach across a lived-in, slightly messy bed in her bedroom, browsing a mobile shopping page on a black smartphone. A house cat jumps onto the bed seeking attention, and she affectionately plays with it. Moments later, a friend calls. She answers, chats, and eventually bursts into laughter. The doorbell rings, so she ends the call and gets up to collect her dinner.
Shot 1 (0–2s):
She is already moving. One thumb scrolls through a shopping page while she frowns slightly, thinking. She quietly mutters in Korean: "아, 뭐 살랬더라…" ("Ah... what was I going to buy again?"). Lips synchronize naturally. Her bare feet gently sway behind her. A low handheld camera glides along the edge of the mattress, with soft bedding partially obscuring the foreground.
Shot 2 (2–4s):
The house cat jumps onto the bed, compressing the blanket as it walks toward her forearm and lets out a single meow. The camera gives a slight jolt from the impact, then quickly reframes from the phone to an over-the-shoulder view that includes her face, hands, phone, and cat.
Shot 3 (4–6s):
She turns warmly toward the cat, stroking it once from its forehead to its shoulders. In a gentle, affectionate tone she says: "우리 애기 왔어?" ("Did my baby come?"). Lip sync is clear and natural. The camera pushes in briefly through the cat's softly blurred foreground toward her face and hand.
Shot 4 (6–8s):
A friend's ringtone sounds. She glances down, confirms the caller, swipes to answer, and brings the phone to her ear. The camera moves in a loose semicircle from a slightly tilted overhead angle, capturing the entire answering motion.
Shot 5 (8–11s):
Her friend begins talking. She responds first with confusion, then disbelief: "어, 왜? 진짜 거짓말." ("Huh? Why? No way, you're kidding."). Immediately afterward she naturally bursts into laughter. The cat kneads the blanket beside her. A close handheld side angle keeps both her phone and profile within the same focal plane.
Shot 6 (11–13s):
A clear doorbell interrupts the laughter. Both she and the cat turn toward the bedroom door. She braces one hand on the mattress to get up. The camera reacts a fraction too late, briefly turning toward the door before naturally correcting back to her rising movement.
Shot 7 (13–15s):
Still on the phone, she hurriedly says: "어, 나 밥 왔다. 끊어." ("My food's here. I'll hang up."). She ends the call with her thumb, gets off the bed, and walks toward the door while the cat follows across the blankets. The camera slides low beneath her elbow and tilts upward as she stands in one continuous motion.
Sound:
No music. Only raw production sound: bedding rustling, quiet breathing, finger taps on the phone, the soft impact of the cat jumping onto the bed, one natural meow, faint purring, a single short incoming ringtone, call connection tone, the friend's voice through the phone, the woman's four Korean lines with accurate lip sync, a genuine brief laugh, one clear doorbell, the tap ending the call, and the soft cat footsteps. No subtitles, no on-screen text, no logo, no watermark. Never render a reference sheet or duplicate the subject.
````

Also in the full library as [SD001](../library/dialogue/SD001.md).

**Run it** — Seedance 2.5 is live on apimodels.app as `seedance-2.5`: $0.120/s at 480p, $0.270/s at 720p, billed on real token usage and charged only on success.

```bash
curl -X POST https://apimodels.app/api/v1/video/generations \
  -H "Authorization: Bearer $APIMODELS_API_KEY" -H "Content-Type: application/json" \
  -d '{"model":"seedance-2.5","prompt":"<the full prompt above>","duration":15,"resolution":"480p"}'
```

Seven shots in 15 s costs $1.80 at 480p, $4.05 at 720p; if you stretch the shot list, `duration` is what moves the bill (4–30 s in one pass, or `-1` to let the model choose). The API exposes 480p and 720p only.

The `@Image 1` here is a person: a raw photo that appears to contain a real person is rejected at create time, so real faces go through the `asset://` portrait library. [Docs](https://apimodels.app/docs/seedance-2-5) · [model](https://apimodels.app/models/seedance-2.5)

---

这条的中文说明:15 秒切成七个带精确秒段的镜头，四句韩语台词要求口型对上，结尾是一整份拟音清单。最后两句是负向约束——不要字幕、不要屏幕文字、不要 logo 和水印，永远不要把参考图本身画出来、不要复制主体——这正是防止参考驱动的任务把参考拼图画进成片的写法。

**用 API 跑这条** — `seedance-2.5` 已在 apimodels.app 上线，命令同上（prompt 换成上面的全文）：480p $0.120/秒、720p $0.270/秒，按真实用量计费，只在成功时扣费。

七个镜头压在 15 秒里：480p 约 $1.80，720p 约 $4.05；要把镜头表拉长，动的就是 `duration`，它也是账单的开关（单次 4–30 秒，或填 `-1` 让模型自己定）；API 只开放 480p 和 720p。这条的 `@图1` 是真人——看起来含真人的原图会在创建时被上游审核拒掉，真人一律走 `asset://` 人像库。文档：[/docs/seedance-2-5](https://apimodels.app/docs/seedance-2-5)
