# Course structure v2 — a few hundred fast lessons, zero hand-holding

**Design law:** the app never explains. Every lesson is a puzzle whose solution *is* the
grammar. The brain is given variation, not instruction — same frame, one thing changes,
you notice what. Scaffolds exist only to die.

## Shape: lessons, not levels

Today: 1 level = 1 puzzle (94 total). New: **1 lesson = a 60–90s burst of 4–6 items**
mixing modes around one micro-goal. ~300 lessons = ~45 units × spiral revisits.
Fast tempo is the feature: item → snap → next, no dead screens between items.

## The five item modes (one drag engine, five retrieval directions)

| Mode | You get | You do | It teaches |
|---|---|---|---|
| **Build** | emoji + sound | assemble jamo → syllable | the script system *(exists)* |
| **Order** | emoji sequence | arrange word tiles SOV | word order *(exists)* |
| **Read** | han sentence only | pick the matching emoji scene | comprehension — han→meaning, the missing direction |
| **Gap** | sentence with one hole | drop the word that fits | slot logic — "that word fits there" *(unparks FILL_LATER)* |
| **Switch** | two sentences, one word apart | tap what changed | minimal-pair perception — the pattern detector |

Every mode is silent: no instruction line after unit 1.

## The generator does the scaling

Hand-writing 300 lessons is a trap. Instead: **frames × tagged lexicon**.
- WORD_BANK words gain semantic tags: `drink, food, animate, place, sky, body…`
- Frames: `[animate] [drink] 마셔요`, `[animate] [food] 먹어요`, `[animate] 자요`,
  `나 [thing] 봐요`, later `[thing] 좋아요`, `나 [place] 가요`.
- The generator fills frames with tag-legal words the learner knows → hundreds of
  correct, fresh sentences; decoys are tag-ILLEGAL words (물 먹어요 is the wrong-feeling
  option — the brain learns selection restrictions by rejecting them).
- Verb inventory grows to ~12 (마셔요 먹어요 봐요 자요 가요 와요 좋아요 있어요 없어요 사요 해요 줘요),
  each carried by a combined emoji, never glossed.

## Phases (the scaffold execution schedule)

**P1 · Letters snap (≈30 lessons)** — 2–3 new words per lesson + an immediate sentence.
Scaffolds alive: romaja under tiles, drag glow, TTS-first. *Glow dies at lesson 8.*

**P2 · Frames (≈120 lessons)** — generated Order/Read/Gap/Switch bursts; subjects and
objects swap constantly; new verbs enter only through frames. *Romaja dies as letters
complete (exists); goal romaja dies here too.*

**P3 · Particles click (≈80 lessons)** — zoom in: 밥 splits into 밥+을, tiles for 은/는/을/를/이/가
snap onto nouns. Gap and Switch carry the whole phase — the particle is always the thing
that changes. No particle is ever named.

**P4 · Off the rails (≈70 lessons)** — scaffold inversion: sound-only Build (emoji appears
*after* you solve — meaning confirms, doesn't lead), Read with longer sentences, mixed
review bursts from the SRS queue. The journal keeps ripening throughout.

## What gets deleted (the hand-holding inventory)

1. Drag glow hint on the correct slot → dies after P1 lesson 8.
2. "drag the letters to build it" instruction lines → first lesson of each mode only.
3. Goal romaja → gone from P2 on (tile romaja already self-destructs per letter).
4. English anywhere → already gone (journal-only).
5. Emoji-first goal → inverted in P4 (sound leads, emoji confirms).

## Build order (each step ships alone)

1. Lesson runner (burst of items + fast transitions) — reuses the review-queue machinery.
2. Tags on WORD_BANK + frame generator + tag-illegal decoys.
3. Read mode, Gap mode, Switch mode (small DOM variants of existing screens).
4. Scaffold schedule (glow/instruction/romaja kill switches by lesson index).
5. P3 particle tiles (the zoom-in — biggest single piece, worth its own pass).

Progress/SRS/journal survive: lessons keyed by stable ids, not array indices (the v2
migration point — do it in step 1 while nobody has progress to lose).
