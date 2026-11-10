---
name: shorts-master
description: The user's unified animated-Shorts skill — every skill they supplied, merged into one pipeline. Idea → fact-checked paradox/con story → performance voice → word timing → shot plan → 3D kit build (bean-head cards in a toon world) with insert beats → stills gate (numbers AND eye) → render → VO-forward mix → independent critic → director fixes → verified delivery. Use for any animated short request: "make a short about...", "video build koro", "Ricks style", "new script", a supplied script or voiceover to turn into a video. Routes that cannot run on this machine (Remotion WebGL, Blender) are documented with their status, never silently substituted.
---

# Shorts Master — all supplied skills, one pipeline

Merged 2026-11-10 from everything the user supplied — **8 skills total** (user's count), make-short's method on top:
1. **cartoon_3d_short** (`~/workspace/custom-skills/cartoon_3d_short/`) — three.js + Remotion route, STYLE_BIBLE look values, impact/kick grammar, look-match loop.
2. **cartoon-audio-short kit** — the WORKING engine on this machine: bean-head canvas cards in a three.js world, headless Chrome, ink + DOF passes. All recent deliveries (Brooklyn Bridge, Cardiff Giant, …) came from it. Two packagings on disk: the 2026-11-06 repack (`~/workspace/cartoon-kit/cartoon-short-kit/`) and the **UPDATED original supplied 2026-11-10 (`cartoon-audio-short111.zip` → `~/workspace/cartoon-kit/cartoon-audio-short/`, vendored at `vendor/cartoon-audio-short/`)** — v2 brings the cast.js/castdefs.js character system (front + SIDE cards, outfit objects), terrain.js heightfields, card depth-pull, route ribbons, thicker ink (5 px near), the render retry loop, and a second worked example ("The Man Who Moved a Mountain", plan at `references/mountain-man-plan.md`). New engine deltas: `references/engines.md` §Kit v2.
3. **claude-animation-skills** (vendored: `vendor/claude-animation-skills/skills/`) — insert grammars: `zach-d-films`, `stick-figure`, `map-route`, `graph`, `breakdown`, `minimalistic-graphics`.
4. **make-short** (`~/workspace/custom-skills/make-short/`) — method: paradox formula, voice-first, gates by numbers AND eye, independent critic + rubric, one-director-per-beat fixes, lessons log. (Its Blender v3 engine does NOT run here — see Engine routing.)
5. **animated_short_style_qa** (`~/workspace/custom-skills/animated_short_style_qa/`) — pre-delivery audit.
6. The user's own Ricks Clips research (Director's Bible `~/workspace/your_files/RicksClips-Directors-Bible.md`) and their standing production rules (below) — these OVERRIDE upstream defaults wherever they conflict.

## The user's standing rules (win over every upstream default)
- **Topic taste:** "interesting" = the Eiffel Tower genre — audacious human con/heist/scheme stories, clever trickster, landmark-scale scam, ironic payoff. Not quirky-animal oddities.
- **Scripts:** the user's own script is used VERBATIM. Facts web-verified before building; disputed counts hedged in the narration itself. Duration follows each request (no standing house length); **voice comfort beats a duration cap** — never push TTS speed to hit a target (Helio 126 ≈ 3.5 w/s was rejected as too fast).
- **Voice:** chosen per build by name. Current stable: **Casper** (`avocado_v2:casper`, F0 ~187–202 Hz = the Ricks band) for new narrations; **MAI_01** = Brooklyn-style builds; **MAI_03** = "Eiffel Tower narrator". Never say the internal voice codes to the user — use display names. A voice is a PERFORMANCE take: per-line speed/pitch variation, intra-line gaps clamped ≤0.28 s, longer pauses only at the pivot and payoff. A flat single-pass take reads as AI and gets rejected. A voice CHANGE after delivery forces a full re-time + re-render — state that cost and confirm first.
- **Captions: ALWAYS on** (overrides the kit's "no captions unless asked"): 2 words at a time, bold white, heavy black outline, and the pivot word(s) on a **red pill**. (make-short's reference measures 1 word at ~70% height; this user's shipped format is the 2-word pair — keep it.)
- **Mix (VO-forward, overrides the kit's −6 dB rule):** bed at **−16 dB**, SFX at **−9 dB** vs the voice's gated RMS, SFX peaks capped 0.7× voice peak. Final file **−14 LUFS ±0.5, true peak ≤ −2 dBTP**, measured IN PLACE on the delivered file. Music is judged by feel: a genre-authentic composed bed, never a generic loop; if music is criticised, change ONLY the music.
- **Characters:** ONE locked design per person (one seed), reused identically in every shot; story upgrades ADD onto the base design. Do not redesign characters to fix a style gap — the open gaps are voice and world, not characters.
- **Worlds:** ONE stable, detailed set per location; the camera reframes inside it. Backgrounds swapping flat sets or shifting palette/lighting mid-location is the #1 past complaint.
- **Camera:** hard cuts + STRONG movement (push-ins, tracks, ECU). Subtle moves read as "no movement". Cuts hide in motion where possible, but a visual break every ~3–4.5 s.
- **Gates:** stills contact sheet to the user BEFORE the long render. After ANY camera change, re-check every placard/text-card frame IN THE FINAL FILE (a cropped "1,000,000 MILES" placard once shipped past the stills gate).
- **Delivery:** file in `~/workspace/your_files/`, verified in place (loudness, silences ≥0.35 s = 0, black/freeze = 0, placards in frame, red pills red). 4K upscale + Dropbox upload (NO share link) only when ordered. Never create a share link the user declined. A cancelled build stays cancelled until the user reverses it.
- **Honesty:** name the gaps that can't be fixed in-pipeline (studio-level 3D polish) instead of overselling. Never self-score a build as "Ricks-like" — report measured deltas.

## Pipeline (every build)
0. **Intake.** Idea, user script, or voiceover? If only "interesting script daw": propose Eiffel-genre topics with verified facts. If the user supplies a script, lock it verbatim.
1. **Facts + story.** Verify facts (sources + caveats noted in the script file header; hedge disputes in-line). Story shape = make-short paradox formula fused with the Ricks skeleton: paradox hook in line 1 (hero + want in frame 1) → stakes → 2–3 escalating beats/reversals, one visible gag per line → "You see," pivot → ironic payoff that resolves the paradox; last frame rhymes with the first. ~3.2–3.4 w/s at performance pace; **deep/soothing narrator voices run ~2.5 w/s — size those scripts at ~2.6 w/s** (kit v2). **Sad beats are never played for laughs (kit v2): on a fall/accident, follow the dropped prop (pot, hat, letter) and keep the person out of frame within ~6 frames.**
2. **Voice first.** Build the performance take (TTS builder pattern: per-segment speed/pitch table → trim −45 dB → gap clamp → A2 VO chain: highpass 75, −1.2 dB @400, +3.5 @3.5k, +2 shelf @9k, compressor 0.06/6/makeup 1.5, limiter 0.7). The picture locks to the voice; NEVER re-time the voice to the picture.
3. **Timing.** `python3 timing.py voice.mp3 script.txt --out work` → `work/words.json`. TOTAL = round(duration×30)+~8. Set `work/warp.json` anchors (identity unless staging was authored on another timeline).
4. **Beat list before code.** One narration line = one beat = one readable frame: line, noun/verb, impact word, frame. Shots are built FROM the beat list (make-short lesson 19: only 9/22 beats were visible when this was skipped).
5. **Build (kit engine, default route).** Clone the freshest delivered project in `~/shorts/` (rsync excl. frames/stills/out/logs/work/caps), then: character system (locked seeds; kit v2 offers `cast.js`/`castdefs.js` with SIDE-view cards + outfit objects for walking/profile stories) → rebuild `web/toon.js` → `web/main.js` worlds (one set per location, ≥10 props per wide, motivated light states in `web/story.js` LIGHTS; kit v2 adds `terrain.js` heightfields + `groundAt()` for hills/cuts) → `web/story.js` shots/cameras/actors/FX → `captions.py` (RED indices = pivot words) → `audio.py` (keep synth defs + gated-RMS lock tail; rewrite the schedule; cues from IMPACT frames, not word starts). **Kit v2 staging laws:** card depth-pull (0.9 m for action cards against walls, 0.3 m otherwise, in BOTH colour and depth materials) so cards never slice into walls; side-view cards need |dot(facing, camera-right)| ≥ ~0.4 or diagonal (~40°) corridor shots; groups of 3–4 never fit side-by-side in portrait — stagger in depth (~5 m / ~10 m); wide action poses get a wider card (1000×1150). See `references/engines.md` for the full recipe and gotchas.
6. **Gate: numbers AND eye.** Render gate stills (every shot's key frames + every text-card frame), build a sheet, LOOK at it yourself, and send it to the user. Numbers: `signalstats` YAVG band [105,135] **measured PER SHOT**, highlights ≥4%, shadow ≤18%. Framing law: portrait hfov ≈ 40% of vfov — two-shots need subjects ≤ ~4 m apart or camera 10 m+ back; check edge-cropping on EVERY still; when unsure, project key points through the camera (`Vector3.project` in Node) before trusting a framing (kit v2). Max ~3 gate rounds.
7. **Render.** 720×1280 (`HASH="#w=720" VW=720 VH=1280 node render.mjs frames "A-B"`), parallel ranges OK when the machine is free; **frames persist across runtime restarts — run renders inside a RESUME retry loop (kit v2: up to ~6 relaunches) and relaunch missing ranges with RESUME=1** (delete a frame's file first to force its re-render; purge stale frames by MTIME CUTOFF between render generations, never by "recent minutes" — a sliding window once let 229 old frames survive into a finish). Story edits made while a render runs only reach frames rendered after it — always re-render an edited shot's range. Lanczos upscale happens in finish.
8. **Finish.** Grade (top-end-only: `eq=brightness=0.005:contrast=1.05,curves=all='0/0.01 0.5/0.52 0.75/0.84 1/0.99'`) → upscale → caption burn → mux `mix_raw.wav` with measured two-pass loudnorm to **−14.0 LUFS in place**. Verify the FINAL file (duration, LUFS/TP, silences, black/freeze, placard frames, red pills).
9. **Independent critic.** A fresh subagent that did NOT build the film scores it with `references/qa-and-critic.md` (rubric: pass = criteria 1–4 ≥7 and mean ≥8). Verify every critic claim at full resolution before acting (critics mis-measure too). Fixes go one director per flagged FRAME RANGE; re-render only that range; redo gate+critic for it.
10. **Deliver + learn.** File + measured specs + honest gaps. Title/description pack in the established pattern. Append new lessons to `references/lessons.md` and durable facts to memory.

## Engine routing (what actually runs on THIS machine)
| Route | Status here | When |
|---|---|---|
| **Kit engine** (three.js in headless Chrome, CPU WebGL swiftshader) | ✅ Working, ~2–7 s/frame at 720p | Default for every build |
| **Route 1 scratch clay-puppet engine** (`~/workspace/ritz-build/scene/`, forked from `~/workspace/route1-sample/`) | ✅ Working, ~1.5 s/frame | The user's OWN-style videos (original clay characters/worlds, no kit assets) |
| **2D PIL/Remotion-flat pipeline** (`~/workspace/ink-test/` pattern) | ✅ Fast | Quick style tests only — user rejected flat looks as "too simple" for finals |
| **cartoon_3d_short Remotion route** | ❌ WebGL context fails in this VM (empty frames) | Only after an environment change; re-run its frame-400 still test first |
| **make-short Blender v3** | ❌ Blender uninstalled at user's order 2026-11-05; VM has no GPU | Only if the user asks to reinstall; its METHOD (gates/critic) is used regardless |
| **make-short legacy 2D Chrome route** | ⚠️ Untested here | Fallback if the kit engine breaks |

## Inserts (spice, 1–2 per short, never a whole video)
From `vendor/claude-animation-skills/skills/` + our kit painters — see `references/inserts.md`:
- **breakdown / graph**: a diagram card that draws the mechanism (our `fxBlueprint` painter in the mix-demo project is the kit-native version).
- **map-route**: a journey beat — route line drawing across a simple map card. **Kit v2 aerial grammar (proven on Mountain Man):** for distances/routes/before-vs-after numbers, go to a true aerial view (camera high, pitched ~75° down, whole route inside the frame width) with a dashed route ribbon that reveals along its length — RED for the long/old way, GREEN for the new way — and repeat the same map angle for the callback.
- **stick-figure**: a 1–2 s white-head stick insert for a sudden explanatory gag.
- **zach-d-films grammar**: slow-motion impact + red force ripple on THE gag frame; anticipation → overshoot → settle.
- **minimalistic-graphics**: clean icon card for a number/date ("£1,000", "50 CENTS" placards are our house version: `fxPlacard`).

## References (in this skill)
- `references/engines.md` — kit build recipe, commands, framing law, every hard-won gotcha.
- `references/voices-and-sound.md` — voice roster + measurements, performance-take method, VO chain, mix locks, SFX density targets.
- `references/inserts.md` — insert grammars and when each earns its place.
- `references/qa-and-critic.md` — gate numbers, the critic rubric, rea-video deltas vs Ricks, delivery checklist.
- `references/ricks-craft.md` — the measured Ricks fingerprint (pacing, cuts, captions, exposure, pitch).
- `references/lessons.md` — running lessons log (seeded from make-short's + ours); append after every build.

## First run under this skill
The 15 s mix demo — "The Man Buried in His Own Invention" (Fredric Baur): project `~/shorts/mixdemo/`, script `~/workspace/your_files/MixDemo-Script.md`. Paradox formula (make-short) + kit engine + blueprint insert (animation-skills) + impact bursts (cartoon_3d_short grammar) + make-short's own SFX files in the mix + Ricks captions/craft + Casper voice.
