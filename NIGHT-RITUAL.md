# Night Ritual — thin slice spec (fortune + bedtime review)

**Thesis:** a 2-minute nightly ritual that feels like superstition and is secretly spaced repetition.
The fortune is SRS in a trench coat. Web-only, no alarm (parked for native), filmable.

## The loop

**Night (after 20:00 local, or `?ritual=1` to force — needed for filming):**
1. Moon button on the map → screen dips into night mode (deep navy, dim, stars; no confetti,
   slow fades, TTS at low rate/volume — "whisper mode").
2. **Calm review** — up to 5 due SRS cards, normal block-assembly interaction, zero
   scoring pressure shown (stars still recorded silently).
3. **The deal** — a fortune card is dealt, face-DOWN, and sealed: "네 운세는 아침까지 봉인됐어 —
   sealed until morning." Sealing = ritual done → feeds the existing streak.
4. Goodnight screen: 잘 자요 + TTS whisper.

**Morning (next calendar day, on open):**
1. The sealed card sits on the map. To break the seal: assemble ONE syllable — the key
   syllable of the fortune (always buildable from letters the user has learned).
2. Card flips: fortune in big Hangeul + emoji, TTS reads it, tap to reveal English.
3. That's the filmable moment: half-asleep person decodes Korean to learn their day.

## Fortune generator (no LLM)

Template bank (~30 entries), slots filled from the user's own learned words:
- **Lucky word** — picked by the SRS scheduler from due/learned words (this is the
  hidden review): "오늘의 행운: 물 💧" (today's luck: water).
- **Lucky number** 1–9 (numbers enter the curriculum later; emoji digits until then).
- **One-line advice** from bank, A0 vocabulary only, 2–4 words max
  ("우유 조심 🥛" — beware of milk). Absurd is good; absurd is shareable.

Key syllable = first syllable of the lucky word.

## Data / reuse

- localStorage `ritual`: `{sealedDate, fortuneSeed, done}` — fortune re-derived from seed
  (deterministic), nothing else stored. Piggybacks existing cloud-sync jsonb.
- Reuse: block-assembly engine, SRS picker, TTS, streak, dev day-offset button.
- New: night palette (~50 lines CSS), 2 screens, fortune bank + generator (~40 lines),
  seal/flip animation, morning gate.

**Estimate: ~1 day, all inside index.html.**

## Parked (explicitly not in slice)

Alarm + AlarmKit (needs Capacitor) · sleep-audio replay (TMR) · push notifications ·
LLM-personalised fortunes · share-card image (fast-follow #1 — the viral artifact) ·
astrology depth (saju theming).

## Success test

Film "I let a Korean fortune app decide my day" with the slice. If the video pulls,
build the alarm + share card. No pull → we spent one day.
