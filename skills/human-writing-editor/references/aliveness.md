# Aliveness - the positive layer

The tell list and the rewrite principles are subtractive: they find slop and cut it. Applied alone, they produce a failure mode of their own - text with nothing wrong and nothing alive in it. Clean, correct, gray. The reader doesn't flag it as AI; they just stop reading.

This file is the additive pass. It runs AFTER the cutting is done (rewrite-principles 1-16) and BEFORE the final length and preserve checks. It never re-introduces a banned shape: everything here works inside the same register rule (one person explaining to one person, out loud).

## The standard

The target is not "text with no AI tells". The target is **the author on a good day**: the version of this text the same person would produce when they had energy, knew exactly what they meant, and cared whether the reader felt it. Same facts, same length, same register. More pulse.

A good check while rewriting: if the author read your output next to their draft, they should think "yes, that's what I was trying to say", not "well, it's cleaner now".

## Beige tells

These are detection patterns for over-cleaned text. Same ID convention as ai-tells.md; the detector and scorer may emit them.

### BEIGE-001 · Dead verb chain

**Pattern:** Almost every verb is a state verb or a bureaucratic bundle: is, has, provides, offers, ensures, "carry out an analysis", "make a decision", «является», «осуществляет проверку», «принимает решение».

**Why beige:** A state verb describes furniture. Readers track actors, so a sentence wakes up when someone in it does something.

**Fix:** Rewrite the load-bearing sentences around the action hiding inside them. "The system performs validation of every draft" becomes "The system checks every draft." "Мы приняли решение о переносе" becomes «Мы перенесли».

### BEIGE-002 · No stake

**Pattern:** The text takes no position anywhere. Every claim would survive a legal review at any company. Reads like minutes of a meeting the author didn't attend.

**Why beige:** A human writing about their own subject always leaks judgment: what matters more, what surprised them, what they'd skip. Zero leakage reads as nobody home.

**Fix:** Find the judgment already implied by the source's facts and state it once, plainly, where it does the most work. If the draft says a feature took three rewrites and now converts 2x, the author plainly thinks the rewrites were worth it - say that. **Guardrail: surface only judgments the source's own facts support. If you have to guess what the author thinks, don't.** Voice-gated: skip for neutral-pro and analyst.

### BEIGE-003 · Flatline rhythm

**Pattern:** Every sentence lands between 8 and 14 words. All declarative, no question, no aside, no sentence that breathes. The opposite failure of TELL-023 (staccato thrust): monotone mid-length instead of monotone short.

**Why beige:** Rhythm is how prose signals what matters. When everything has the same weight, nothing does.

**Fix:** Give the single strongest claim the shortest sentence in the piece. Give the most involved reasoning one long sentence that holds together spoken aloud. Leave the rest alone; the point is contrast, not choreography.

### BEIGE-004 · Hollowed-out claims

**Pattern:** The slop was cut and nothing replaced it, leaving bare assertions: "The product works well and users like it." "Команда сильная, результаты хорошие."

**Why beige:** The fog at least gestured at content. The hollow version admits there isn't any.

**Fix:** Pull the most concrete detail available in the source (a number, a named user, an event, a before/after) and let it carry the claim. If the source truly contains nothing concrete, sharpen the claim itself until it says something falsifiable, and keep it short.

### BEIGE-005 · Most-probable-word syndrome

**Pattern:** Every content word is the statistically safest choice: improve, important, effective, situation, aspect, solution, «улучшить», «важный», «эффективный», «ситуация». No word in the text would surprise an autocomplete.

**Why beige:** Precision lives in the less probable word. "The onboarding leaks users" tells you more than "the onboarding could be improved", and it's shorter.

**Fix:** Find the one or two load-bearing spots (usually the main verb of the main claim, and the noun the piece is actually about) and replace the generic word with the one the author would use out loud, drawn from the source's own domain. One vivid word per piece is seasoning; five is costume. **The unexpected word must be MORE precise than the one it replaces, never decorative.**

## Techniques

Apply in this order of preference; stop when the text has a pulse. Adding all of them to one short piece is its own kind of slop.

1. **One image.** The most abstract key claim gets one concrete picture: a number, a scene, a named thing, a before/after. Material must come from the source or undisputed common ground. One image well-placed beats three scattered.

2. **Verbs do the lifting.** Audit the main claims for BEIGE-001. Energy added through verbs survives every register, including formal ones; this is the safest technique on the list and usually the highest-yield.

3. **Shortest sentence on the strongest claim.** See BEIGE-003. This is free: no new content, just redistribution of weight.

4. **State the stake.** One plain sentence of judgment where the voice allows it (operator, founder, creator, casual, custom voices). See BEIGE-002 and its guardrail.

5. **First sentence earns its place.** It must contain something the reader didn't already assume: a number, a tension, a position. This is content, not a hook - "Here's what nobody tells you" is banned (TELL-019); "We rewrote the onboarding three times before it converted" is an opening.

6. **One human seam, maximum.** A parenthetical aside, a brief self-correction, a plain admission of limits ("this only worked because the list was small"). One per piece, only in casual-leaning voices, only if the source's author plausibly would. Two seams read as performance.

## Guardrails

- **No invention.** Aliveness never adds facts, numbers, anecdotes, or opinions the source doesn't support. When the source is thin, the honest move is a shorter, sharper text, not a decorated one.
- **No performance.** Every technique output must still pass the say-it-aloud test from rewrite-principle 0. If a line got livelier but now sounds performed to an audience, revert it.
- **Voice gates.** neutral-pro and analyst take techniques 1, 2, 3, 5 only. All other voices take the full list. Shakespeare is exempt from this file entirely.
- **Strictness.** `light`: fix only flagrant BEIGE (a whole piece of dead verbs, a completely hollow claim). `standard` and `aggressive`: full pass. Aggressiveness applies to cutting, never to adding drama.
- **Length band still holds.** Rule 17 (70-130% of source) is unaffected; aliveness mostly redistributes words rather than adding them.

## Order of operations (updated cheat sheet)

```
FRAME TASK -> DETECT -> CUT FILLER -> REPLACE ABSTRACTIONS -> FIX RHYTHM
    -> REMOVE TRANSITIONS -> KILL REFRAME COUPLETS -> REWRITE ARROW STEPS
    -> APPLY VOICE
    -> ALIVENESS PASS (this file: beige check + techniques, voice-gated)
    -> CHECK PARAGRAPH-RHYTHM VARIETY -> CHECK LAST LINE
    -> CHECK LENGTH IN BAND -> CHECK PRESERVE LIST -> SCORE
```
