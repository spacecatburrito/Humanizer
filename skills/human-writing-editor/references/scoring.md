# AI-ness Scoring

Score 0–10 across eight dimensions. Final AI-ness = average rounded to nearest integer.

---

## Scale

| Final score | Reading |
|---|---|
| 0–2 | Reads as natural human writing. |
| 3–4 | Mostly fine. Minor polish residue. |
| 5–6 | Noticeable AI influence. Several tells present. |
| 7–8 | Strong AI patterns. Multiple categories firing. |
| 9–10 | Obviously AI-generated. |

---

## Dimensions

Score each 0–10 (lower = more human).

### 1. Generic phrasing

How much of the text is corporate-fog vocabulary (TELL-004) or buzzword stacking (TELL-020)?
- 0 = none
- 5 = several abstract verbs / buzzwords without concrete meaning
- 10 = almost every sentence has at least one fog word

### 2. Structural predictability

Symmetric sentences, rule-of-three lists, parallel clauses, balanced bullets (TELL-009), or adjacent mirrored two-sentence splits (TELL-027)?
- 0 = irregular, varied
- 5 = visibly patterned in places; one mirrored twin-sentence pair is acceptable, two or more is a tell
- 10 = uniform throughout, multiple mirrored twin-sentence pairs in the same piece

### 3. Word-choice abstraction

Specific nouns/verbs/numbers vs. abstract claims (TELL-013)?
- 0 = concrete, named, quantified
- 5 = mix
- 10 = abstract throughout, no named entities or numbers

### 4. Tone neutrality

Personality vs. neutral-bot tone?
- 0 = clear voice and POV
- 5 = generic professional
- 10 = no perceivable author

### 5. Formatting / punctuation tells

Em dashes (TELL-001), fragment chains (TELL-005), setup colons (TELL-019), forced bullets, emoji clusters?
- 0 = clean
- 5 = a few visible tells
- 10 = formatting *is* the AI signal

### 6. Opening / closing clichés

Generic openings (TELL-003), forced conclusions (TELL-007), motivational closers, em-fragment closers (TELL-016)?
- 0 = both ends land naturally
- 5 = one end is templated
- 10 = both ends are pure template

### 7. Spoken-register failure

Would each sentence survive being *said aloud to one person's face*, or does it only work as written performance for an audience? This is the generative counterpart to the named tells — it catches novel slop the TELL list doesn't enumerate (see rewrite-principle 0).
- 0 = every sentence would survive being said to one person
- 5 = several sentences are written-performance shapes (build-ups, reveals, audience-address)
- 10 = nothing conversational; the whole piece is performed for an audience

### 8. Flatness (beige)

The over-cleaned failure mode: no classic tells, no pulse either. Scored against aliveness.md (BEIGE-001…005): dead verb chains, no stake anywhere, flatline rhythm, hollowed-out claims, every word the most probable one.
- 0 = the text has a pulse: weighted rhythm, action verbs, at least one concrete image, a discernible author
- 5 = competent but gray; a reader would skim without retaining anything
- 10 = minutes-of-a-meeting prose; nothing wrong, nothing alive

Note: this dimension catches texts that score well everywhere else. A piece with sub-scores of 1 on dimensions 1–7 and 8 here is NOT done — it's beige, and the rewrite should run the aliveness pass.

---

## Output format for `check` and `score-only` modes

```
AI-ness: 7/10

Sub-scores:
- Generic phrasing: 8
- Structural predictability: 7
- Word abstraction: 8
- Tone neutrality: 6
- Formatting tells: 7
- Opening/closing: 6
- Spoken-register: 7
- Flatness: 3

Top issues:
1. [TELL-002] Fake contrast formula in line 1
   Excerpt: "It's not just X — it's Y"
   Fix: state Y directly.
2. [TELL-004] Corporate fog: "leverage", "robust", "ecosystem"
   Excerpt: "leverage our robust ecosystem"
   Fix: replace with concrete actions.
3. [TELL-001] Em dashes used 4× in 3 paragraphs
   Fix: replace with periods/commas.

Fix direction: cut openers, kill em dashes, replace abstract verbs with concrete outcomes.
```

For `rewrite` mode: do not show this block. Output rewritten text only.
