# Engines — build recipes and gotchas

## Kit engine (DEFAULT — cartoon-audio-short kit)
Source: `~/workspace/cartoon-kit/cartoon-short-kit/` (engine, tools, worked example). Working projects live in `~/shorts/<slug>/`.

### Clone recipe (per project)
```
rsync -a --exclude='frames' --exclude='stills*' --exclude='out' --exclude='*.log' \
  --exclude='work' --exclude='caps' --exclude='gate*' ~/shorts/<freshest-delivered>/ ~/shorts/<new>/
```
Clone the FRESHEST delivered project (its main.js/story.js carry the latest fixes), not the raw kit. Then rewrite: `script.txt`, voice, `web/story.js`, the worlds in `web/main.js`, outfits in `web/roman.js`, `audio.py` schedule, `captions.py` RED set.

### Voice → timing
- Performance VO builder pattern: `~/workspace/cardiff-build/build_voice_cardiff.py` (per-segment speed/pitch, trim at −45 dB, gap clamp ≤0.28 s, concat with authored gaps). Then the A2 chain (see voices-and-sound.md) → project `voice.mp3`.
- `python3 timing.py voice.mp3 script.txt --out work` → `work/words.json` (keys w/s/e per word). TOTAL = round(last word end × 30) + ~8.
- `work/warp.json`: identity `{"anchors": [[0,0],[TOTAL,TOTAL]]}` when staging is authored on the render timeline (warpF = identity in story.js).

### Code rules (learned the hard way)
- **Rebuild `web/toon.js` after ANY edit to `toonbase.js` or `roman.js`**: `cat web/toonbase.js web/roman.js > web/toon.js`. Forgetting this crashed a build ("reading 'skin'").
- Grep for identifier collisions before adding names to toonbase/roman (single module scope after concat).
- Painters (FX cards) live at the END of `roman.js`; characters via `R(T, outfitKey, opts, pos, extra)` → `romanFront`; card = 1200×2000 canvas, design 600×1000, soles y=975, 2.25 m tall, yaw-billboard only. Animated FX must vary their cache KEY every frame (key = name + frame-derived value).
- DECK = 6 is the actor-ground constant in every project so far.
- `textSign()` in main.js returns a **MeshToonMaterial** — pass it directly as `add()`'s material argument; wrapping it renders pure black.
- A placard's drawn rect is ~484/600 of the 1.35 m-wide card (≈1.09 m at scale 1.0); an FX card's drawn centre sits at pos.y + ~1.125×scale when the drawing is centred on the design canvas (500/1000).

### Framing law (portrait)
- Portrait hfov ≈ 40% of vfov; half-hfov ≈ 10–13° at fov 33–42. Horizontal half-width at distance d ≈ d·tan(hfov/2).
- Two-shots: subjects ≤ ~4 m apart, or camera 10 m+ back. Placards/FX cards within ~1 m lateral of the camera axis at their depth.
- A card placed "beside" a character at close camera distances slides out of frame as the camera pushes/pulls — verify the card at the FIRST, MIDDLE and LAST frame of its window, in the FINAL file (Cardiff newspaper card needed 3 passes; shortening its window fixed the pull-back drift).
- Check edge-cropping on EVERY gate still.

### Browser / render
- Browser: Remotion's Chrome Headless Shell symlinked into the ms-playwright cache (Playwright's own download stalls; /opt/meta-chromium refuses, exit 13).
- Render at 720×1280: `HASH="#w=720" VW=720 VH=1280 node render.mjs frames "A-B"` (also used for gate stills into a named dir). ~2–7 s/frame alone; much slower under parallel load — on this 1.5-CPU box, 3 parallel ranges can be SLOWER per frame than 1–2. Runtime restarts kill render processes but frames persist: count `frames/*.jpg`, relaunch missing ranges with `RESUME=1`. RESUME skips existing files — DELETE a frame file to force its re-render.
- Don't run heavy Python while rendering on this box.

### Finish (per project, adapt finish_cardiff.sh)
1. `ffmpeg -i mix_raw.wav -af loudnorm=I=-14:TP=-1.5:LRA=7 -ar 48000 -ac 2 mix.wav` (if a measured pass lands ≈−15.3 or under-gains, do a second measured pass with offset → −14.0).
2. Frames → film: `-vf "scale=1080:1920:flags=lanczos, eq=brightness=0.005:contrast=1.05, curves=all='0/0.01 0.5/0.52 0.75/0.84 1/0.99'"` libx264 crf 17.
3. Caption burn: caps/c*.png inputs + `caps/filter.txt` (from captions.py).
4. Mux with explicit `-map 0:v:0 -map 1:a:0`, `-shortest`, faststart. Copy to `~/workspace/your_files/`.
5. Verify IN PLACE: ffprobe duration/size; ebur128 I + peak; silencedetect (−45 dB, 0.35 s) = 0; blackdetect/freezedetect = 0; extract every placard/FX frame + red-pill caption frames and LOOK.

### Audio (audio.py pattern)
Keep the synth defs + the gated-RMS lock tail; rewrite only the schedule. Cues at IMPACT frames. Bed −16 dB / SFX −9 dB vs voice gated RMS; SFX peak cap 0.7× voice peak. SFX density target ≈ Ricks (see ricks-craft.md). Music stops/thins at the pivot; a low sting lands on the payoff word.

## Route 1 scratch clay-puppet engine (user's OWN style)
- Code: `~/workspace/ritz-build/scene/` (forked from `~/workspace/route1-sample/`); NOT the kit — original clay-puppet characters + procedural worlds, dive-in opening + pull-out ending, single signal-red accent, red stamp on the ending.
- Render ~1.5–1.7 s/frame at 720×1280 SINGLE process (3 parallel processes were ~8× slower from CPU oversubscription — run ONE).
- First full delivery: `The_Man_Who_Tried_to_Sell_the_Ritz.mp4` (2026-11-10).

## Routes not runnable here (status, not excuses)
- **cartoon_3d_short (Remotion)**: WebGL context creation fails in this VM (empty sky-colour frames; /opt/meta-chromium refuses under Remotion). Its STYLE_BIBLE values still inform look targets. If the environment changes, re-run its frame-400 still test before promising anything. Its upstream user rules (no captions, 2K export, music +3 dB) apply ONLY to that route's upstream projects, not to this user's builds.
- **make-short Blender v3**: needs Blender 5.x + GPU. Blender was installed 2026-11-04 and removed 2026-11-05 at the user's order; do not reinstall unless asked. DaVinci Resolve also cannot run here (needs 32 GB RAM + discrete GPU; VM has ~7.7 GB, no GPU).
- **GitHub Actions 3D route** (user 0xskylite1 / Meat-shower-3d): gate passed 2026-11-04 but the full build was DECLINED by the user ("No dorkar nai") — do not revive unless asked.

## Kit v2 deltas (cartoon-audio-short111, supplied 2026-11-10)
Canonical copy: `~/workspace/cartoon-kit/cartoon-audio-short/` (also vendored in this skill). Worked example #2: "The Man Who Moved a Mountain" (41.8 s, 12 shots) — full plan in `references/mountain-man-plan.md`; study it before planning any journey/labor story.
- **Cast system**: `web/cast.js` + `web/castdefs.js` replace roman.js (`cat toonbase.js cast.js > toon.js`). `bodyFrontX`/`bodySideX` painters — SIDE-view cards exist. Outfits are plain objects (top/kurta/dhoti/sari/pagri/hair/beard/skin/build fields). Wide action poses (two-handed swing) need a 1000x1150 card, soles at DH-25.
- **Card depth pull**: shift card vertices toward the camera in view space (`mv.xyz *= (d-pull)/d`, screen size unchanged) in BOTH the colour and the normal/depth card materials — pull ~0.9 m for action cards against walls, 0.3 m otherwise; pull FX hit points by the same amount. Without it, a yaw billboard next to a wall slices into it and props vanish inside rock.
- **Side-view law**: keep |dot(facing, camera right)| >= ~0.4; corridors/cuts shot diagonally (~40 deg off axis), tool/gaze toward screen-right where the target is.
- **Terrain**: `web/terrain.js` ridge+cut heightfield with `groundAt(x,z)`; clamp cameras above groundAt+1.2 and check the sightline clears the near lip.
- **Ink**: width ~5 px near -> ~3.2 px far at 1080 (2.5 px is too thin; DOF washes it). Debug with `window.INKDBG` + readRenderTargetPixels. Depth target is FloatType RGBA cleared to alpha 0; shaders read alpha <= 0 as far (1e5). Near-side depth ink = second difference of 1/z along 4 directions (exactly 0 on any plane, so no false lines on grazing ground); diagonal steps count at sqrt(2) distance.
- **Materials**: MeshToonMaterial ignores flatShading — use non-indexed polyhedra (Dodecahedron/Icosahedron detail 0) for faceted rocks. Triplanar toon: inject world pos/normal at worldpos_vertex, replace map_fragment, own customProgramCacheKey.
- **Sky/ground**: three-stop sky (a two-stop blue->peach gradient turns purple); fade ground texture detail to its mip average beyond ~70-320 m or wides tile visibly.
- **Audio layout**: run inside the project's `audio/` folder (`audio.py`, then `mix.py` -> `audio/mix.wav`; finish.sh reads it). Continuous beds (wind/ambience) dominate the SFX stem's gated loudness — keep them low; after the peak cap, SFX landing at -6 to -8 dB vs voice is right (USER OVERRIDE still wins for final balance: bed -16 / SFX -9). Big hits are layered: steel tink + rock crack + low thump + debris rattle.
- **Finish**: frozen spans >=0.4 s are usually a camera that settles after an event — add a creeping push to the shot's end and re-render only its frames. Cap white flashes at ~0.9 so no frame is pure white.
- **Render ops**: retry loop `for i in 1..6: RESUME=1 node render.mjs ... && break` (the environment restarts mid-render); stay in the turn with foreground waits <=10 min printing frame counts; story edits during a render only reach frames rendered after it — re-render the edited range afterwards.
