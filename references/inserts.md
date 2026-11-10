# Insert grammars (from claude-animation-skills, vendored in ../vendor/)

An insert is a 1–3 s change of visual grammar inside a kit build. One or two per short; the gag or the mechanism must NEED it. Full sources: `vendor/claude-animation-skills/skills/<name>/`.

- **breakdown** — the mechanism, exploded: parts separate, labels point. Kit-native version: a painter card (e.g. `fxBlueprint` in `~/shorts/mixdemo/web/roman.js`: deep-blue sheet, white line art, dimension arrows, one gold accent line). Use when a line explains HOW something works.
- **graph** — a number made visible: bars/heights drawing up on a plain card. Use for prices, counts, distances ("£1,000", "2.3 million gallons"). Our house version for diegetic numbers is `fxPlacard` (cream card, ink border, serif).
- **map-route** — a journey: simple coastline/landmass card, route line draws itself, dot travels. Use when the story moves place ("he sailed to Australia to sell it again").
- **stick-figure** — big-white-head stick people on a flat ground line, 1–2 word captions, whip transitions, impact = burst + shake + flash. Use as a sudden deadpan flashback gag, never for a whole Ricks-style video.
- **zach-d-films grammar** — 3D explainer beats: slow-motion approach, RED FORCE RIPPLE on contact, freeze on the impact frame + KICK. In kit builds this is `fxBurst` + a story.js KICKS entry at the impact frame + an SFX hit timed to the FRAME, not the word (make-short lesson 29: a pop 3 frames early reads wrong).
- **minimalistic-graphics** — one icon, one word, lots of air. Use for dates and verdicts ("5 YEARS", "COMPLETE FANTASY." — the Route 1 engine renders this as the ending red stamp).

Timing law for all inserts: the insert's readable frame must land ON its cue word (±0.25 s), the gag frame stays CLEAN (no whip/puff/blur on it), and a 12–24 frame reaction hold follows (make-short lessons 9, 20).
