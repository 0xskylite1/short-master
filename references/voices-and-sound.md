# Voices and sound

## Voice roster (measured, not guessed)
| Voice | ID | Measured F0 | Use |
|---|---|---|---|
| Casper "Confident Trumpet" | avocado_v2:casper | ~187–202 Hz | Default new narrator (user pick 2026-11-10). Pitch sits IN the Ricks band — closes the pitch gap at the source |
| Aria (MAI_01) | avocado_v2:MAI_01 (display name only to user) | — | Brooklyn-style builds exactly as specified |
| Helio (MAI_03) | avocado_v2:MAI_03 | ~108 Hz | "Eiffel Tower narrator" when the user names it |
| Wry Noodle | avocado_v2:vdc_31875 | ~158 Hz | Sampled, not picked — funny/wry alternate |
| Satiny Moon | avocado_v2:miles | ~90 Hz | Sampled, not picked — funny but pitch goes the wrong way |

Rules:
- Voice follows what the user names PER BUILD. Never say internal codes ("MAI_01") to the user.
- Processing cannot fix pitch: +3 semitones on Helio reached only ~137 Hz vs Ricks 186–203 Hz; beyond +4 sounds cartoonish. Pick the right source voice instead.
- "Brad" (ElevenLabs) is a dead end without the user's account: 8+ voices share the name, none publish pitch. Don't order by name.
- TTS: `/opt/hatch/bin/tts speak --text ... --voice <id> --speed 1-200 --output ...`. Full catalog: `/opt/muse/assets/voice-selector/voice_source.json`.

## Performance take method (a flat take gets rejected as "AI feel")
- Per-segment speed/pitch table (builder: `~/workspace/cardiff-build/build_voice_cardiff.py`): speeds vary ±10 around the base, pitch 0.99–1.02 per line.
- Casper articulates ~3.6 w/s at speed 115 on long lines but is dramatic/pausey: Cardiff needed speeds +20 (116–132) to land 2.91 w/s overall. Calibrate on one long line before the full take.
- Trim silence at −45 dB; clamp intra-line gaps to ≤0.28 s (Ricks phrase-gap p90 is 0.22–0.28 s; raw TTS runs ~0.42 s). Authored pauses: ~0.5 s before "You see,", ~0.45 s before the payoff line.
- asetrate pitch trick needs `aresample=44100` BEFORE `asetrate` in the ffmpeg chain.
- Pitch-shift in the builder: `aresample=44100,asetrate=44100*<pitch>,aresample=44100`.

## VO chain (A2 recipe, applied to the assembled take)
`highpass=f=75, equalizer 400 Hz −1.2 dB, equalizer 3.5 kHz +3.5 dB, highshelf 9 kHz +2 dB, acompressor threshold 0.06 ratio 6 makeup 1.5, alimiter limit 0.7`

## Mix locks (USER rules — override the kit's −6 dB house rule)
- Bed at −16 dB and SFX at −9 dB vs the voice's gated RMS (0.4 s blocks, keep blocks > 5% of max). SFX peaks capped at 0.7× voice peak. (The kit's −6/−12 balance masked the narration; the user had to ask for the voice up.)
- Final: −14 LUFS ±0.5 integrated, true peak ≤ −2 dBTP, verified on the delivered file in place. Loudnorm single-pass often under-gains (~−15.3): use a measured two-pass with offset.
- Ricks audio fingerprint: zero silences ≥0.4 s; crest 4.6–6.5 dB; SFX ~74 events/min (our Abagnale test hit 65 — density still slightly short); rea-video detects NO music bed in Ricks originals vs a clear bed in ours — keep the bed sparse and low.
- Music by feel: genre-authentic composed bed (folk plucks for 1800s, music-box for whimsical, etc.). If the user criticises the music, change ONLY the music stem.
