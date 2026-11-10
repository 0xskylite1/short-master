# QA gates and the independent critic

## Gate 1 — stills (before any long render)
- Stills at every shot's key frames + EVERY text-card/placard frame + first/middle/last frame of each FX window.
- Numbers (signalstats over the frames / sampled final): YAVG mean in [105, 135]; highlights (≥235) ≥ 4%; shadow (≤16) ≤ 18%. Ricks originals: YAVG ~120, highlights ≥4.1%. Our pre-fix builds ran YAVG 73–83, highlights 0.6–1.8% — the exposure gap was the single biggest measured look difference.
- Eye (make-short lesson 1: passing numbers is not passing): gag object visible and BIG at its word; faces readable (heads 30–40% of frame height in character shots, dialogue 45–80% in Ricks MCUs); nothing cropped; text not mirrored; characters not overlapping; mood colour right; no giant foreground clutter; props near the camera path re-checked after every camera move.
- Send the sheet to the user before rendering.

## Gate 2 — final file, in place (never trust the pre-mux numbers)
- ffprobe: 1080×1920, expected duration ±0.1 s.
- ebur128: integrated −14 ±0.5 LUFS; peak ≤ −2 dBTP.
- silencedetect (−45 dB, d=0.35) = 0; blackdetect = 0; freezedetect (d=0.4) = 0.
- Extract and LOOK at: every placard frame, every red-pill caption (pill actually red), the hook frame, the payoff frame.
- Script↔visual check: every narration line's noun/verb visible at its word (line-by-line pass, like Cardiff's 14/14).

## The critic (make-short step 6 — never self-score)
Spawn a FRESH subagent that did not build the film. Give it: the final mp4, the reference (if any), this rubric, and your suspicions to verify. It extracts 4 fps frames + matched sheets, fills scores with evidence, and returns top-3 fixes by FRAME RANGE (<400 words). Pass bar: criteria 1–4 each ≥7 AND mean ≥8. Verify every claim at full resolution before acting (lesson 28: the critic once mis-measured caption size by 2.5×).

| # | Criterion | 10/10 means |
|---|---|---|
| 1 | Character acting | squash/lean/anticipation, ≥2 pose changes/s speaking, 0.4–0.8 s reaction holds |
| 2 | Face size | heads 30–40% frame height in character shots; <5% of frames below 15% |
| 3 | Sharpness | blur only on declared whips; beat frames sharp (lapvar) |
| 4 | Beat on screen | every line's noun/verb visible, ≥25% of frame, at its word ±0.25 s |
| 5 | World richness | one stable set per location, ≥8–12 props per wide, painted textures, ink |
| 6 | Grade | exposure in band, motivated moods, no mood graded onto inserts |
| 7 | Comedy timing | gag lands clean, then 0.5–1 s hold on the reaction face |
| 8 | Camera variety | size change every 2–3 s; calm eased moves; variety from cut points, not constant whips |
| 9 | Captions | house format (2-word pairs, red pivot pill), on the word |
| 10 | Sound sync | impacts within ±2 frames of the visible hit; no missing hits |

## rea-video (measured deltas vs Ricks, 2026-11-09)
`~/workspace/rea-video` (prefix PATH with ~/.local/bin). `rea-video decompose <video> -o <out> --lang en` (~5–6 min/short; no VLM configured — pair with your own storyboard check; the tool alone mislabels formats).
Reference points: Ricks original vs our 1:1 remake — cuts 11.0/min vs 28.8; avg shot 5.32 s vs 2.02 s; SFX 80 vs 66 per short; text events 135 vs 108; music bed NOT detected in Ricks. Abagnale test fixes moved: MCU share 26%→50%, text events 113→130/min, exposure floor fixed. Still open after that test: voice pitch (fixed later by Casper at the source), SFX density ~12% short.

## Delivery checklist
File in `~/workspace/your_files/` + specs (duration, LUFS/TP in place, silence/black counts) + title pack (`<Topic>-TitlePack.md`: verb-first recommended title, 4–5 alternates, copy-paste description with hedges intact, thumbnail text). 4K + Dropbox only on order, never a share link unless explicitly asked.
