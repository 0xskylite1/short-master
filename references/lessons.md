# Lessons log — append after every build (one line each: what was found, what fixed it)

Seeded 2026-11-10 from make-short's lessons.md (86 lines, kept in full at
~/workspace/custom-skills/make-short/references/lessons.md) and this user's build history.

## From make-short (binding)
1. Passing numbers is not passing — LOOK at every still next to the reference.
2. Don't grade a mood onto a macro insert; faces/labels/props keep real colours.
3. Whips ~6 frames; long whips smear ~15% of a film.
4. Faces 30–40% of frame height in character shots; a wide lasts ~1 s in 9:16.
5. Build the shot list FROM the beat list — one beat, one readable frame (only 9/22 beats were visible when skipped).
6. Gag frames stay clean; 12–24 frame reaction hold after each gag.
7. Self-rating inflates ~2 points — independent critic only.
8. Verify the critic at full resolution before acting on a claim.
9. Time SFX to the visible impact frame, not the word start.
10. A hero prop must read as itself at phone size.
11. Refer to shots by FRAME RANGE; shot ids change when shots.json is rewritten.
12. Quote ETAs at 1.5×; per-shot saturation boosts cap at ~1.2; each agent diffs against the approved baseline before reporting.

## From this user's builds
13. After cloning a project, verify word-field names against the NEW timeline.json before stills QA.
14. `pageCard`/`stampMark` (2D route) are origin-centred; stills QA must include every text-card beat.
15. Kit render: RESUME=1 skips existing frames — delete a frame file to force its re-render; runtime restarts kill renders, frames persist.
16. Portrait hfov ≈ 40% of vfov: two-shots ≤ ~4 m apart or camera 10 m+ back; check edge-cropping on EVERY still.
17. After ANY camera change, re-check every placard/text-card frame in the FINAL file (cropped 1,000,000 MILES placard; Cardiff newspaper card drifted out during a pull-back — shorten the window or track the axis).
18. Mix: bed −16 dB / SFX −9 dB vs voice — the kit's −6/−12 masked narration for this user.
19. Voice pitch is a SOURCE choice (Casper), never a processing fix.
20. One stable set per location + one locked character design (seed) — the user's two most repeated complaints were set-swapping and character drift.
21. Mux with explicit -map; loudnorm-measure the FINAL file in place (a wrong-audio copy once shipped at −28 LUFS).
22. Attachments must live under ~/workspace/ to display (copy gate sheets into your_files or the project dir inside workspace).
23. A voice change after delivery = full re-time + re-render; state the cost first.
24. Music changed alone when criticised; never touch voice/picture/timing in the same pass.
25. Measure exposure PER SHOT, not just the global mean — the mix demo's global YAVG 106 hid lab shots at 91–99 (critic caught it).
26. An FX burst is only real if it's IN FRAME at its frame: the f62 lid-pop fired above a too-tight push-in and simply doesn't exist on screen. Gate-check every FX window's frames against the FINAL camera path.
27. (kit v2) Cards slice into walls without depth pull — pull action cards 0.9 m toward the camera in both colour and depth passes.
28. (kit v2) Ink at 2.5 px washes out under DOF; use ~5 px near tapering to ~3.2 px far at 1080.
29. (kit v2) A frozen span in finish QA usually means the camera settled after an event — end every shot with a creeping push.
30. (kit v2) Groups of 3-4 never fit side-by-side in a portrait frame; stagger in depth (~5 m front, ~10 m back) and put the gag on a fully visible character.
31. (kit v2) Sad beats: follow the dropped prop, person out of frame within ~6 frames; never play a fall for laughs.
32. Purge stale frames between render generations with a FIXED mtime cutoff placed between the two generations — a sliding "last N minutes" window overlaps the previous render and lets old frames survive a RESUME finish (mix demo: 229 v1 frames hid inside the v2 finish; caught only by a final-file frame check at the blueprint window's end).
