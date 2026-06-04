# Rewrite Principles

Apply in order. Earlier rules override later ones.

---

## 0. Frame the task before you touch a sentence

Set the register and the goal first. This is the difference between a clean rewrite and a *polished-slop* rewrite, and it's why ordinary chat sounds human while "posts" don't: the post register is itself saturated with these tells, so scrubbing tells off it isn't enough — reconstruct the register that was never sloppy.

- **Register: one person explaining to one person.** Rewrite as if the author is telling the point to a single smart, busy reader who will be irritated by padding — a DM or a said-out-loud explanation, not a piece performed for an audience.
- **Goal: be understood, not be impressive.** Optimising for "sounds impressive" is what *generates* the tells (reveals, tricolons, em-dash drama, motivational closers). Optimise for "the reader gets the point with the least friction."
- **The rewrite trap.** "Improve this post" silently re-invokes the polished-post register, so the model re-adds slop even while obeying the tell blacklist. Counter it explicitly: you are not making it a better *post*, you are making it sound like the author *saying* it.
- **Say-it-aloud test.** If a sentence would feel performed when said to one person's face, flatten or cut it. Anything that only works as written performance fails.

This rule sets the target; rules 1–16 are how you hit it. When a later rule and this register pull apart, keep the register.

---

## 1. Cut before you add

Remove filler before rewriting. Most AI text gets better just by deleting:
- corporate padding (TELL-008)
- generic openings (TELL-003)
- importance phrases (TELL-006)
- forced conclusions (TELL-007)
- adverb crutches (TELL-014)
- praise prefaces (TELL-011)
- hedging stacks (TELL-017)

Only add new wording when cutting alone leaves something incomplete.

---

## 2. Replace abstraction with specifics

Abstract verbs (leverage, unlock, streamline, foster) → concrete actions.
Vague nouns (engagement, value, impact, solutions) → named outcomes with numbers when possible.

| Abstract | Specific |
|---|---|
| "We help optimize user engagement" | "We get more first-time users past day 7" |
| "Drives meaningful results" | "Cuts onboarding time from 4 days to 1" |
| "Powerful insights" | "We saw users open the app 3× more on weekends" |
| «Повышаем эффективность работы» | «Сокращаем время согласования договора с 5 дней до 1» |

If you don't know the specific number/outcome, ask the user or rewrite around what's actually claimed.

---

## 3. Break predictable rhythm

AI defaults:
- Uniform sentence length
- Symmetric clauses
- Rule-of-three lists for everything

Mix:
- Short statements (3–8 words)
- Medium explanations (10–18 words)
- Occasional longer sentences when one idea genuinely needs space

Target distribution for prose: roughly 30% short, 50% medium, 20% long. Don't measure literally — feel the rhythm.

For lists: vary item length. Don't make all three bullets the same shape.

---

## 4. Remove default transitions

Cut: However · Moreover · Additionally · Furthermore · In addition · Notably · On the other hand.
RU: Однако · Более того · Кроме того · Помимо этого · Стоит отметить.

Replace with:
- Direct continuation (next sentence picks up the thread).
- A new paragraph if the shift is real.
- Restructure if the transition is the only glue (the underlying connection is probably weak).

Allowed sparingly: But, And, So, Yet, Still — at sentence start, in moderation.

---

## 5. Preserve meaning, not form

Don't paraphrase clause-by-clause. Read the source, identify the actual claim, rebuild the sentence around it.

A good rewrite often:
- changes sentence count (1→2 or 2→1)
- moves the main verb earlier
- swaps subject for the actual human/team/product

A bad rewrite keeps structure and changes synonyms — that's paraphrasing, which produces worse AI text.

---

## 6. Allow sharpness

Human writing is more direct than AI default. Permitted:
- Strong claims (when justified by source).
- Removed hedging.
- Opinion in voice profiles that allow it (`founder`, `operator`, `creator`).
- Skepticism, irony, pushback against industry clichés.

Not permitted:
- Inventing claims the source doesn't make.
- Adding opinions in `neutral-pro` or `analyst` voice.

---

## 7. Active voice with human subject

Find the actor. Make them the subject.

| Passive / inanimate | Active human |
|---|---|
| "The decision was made" | "We decided" |
| "Mistakes were made" | "We made mistakes" |
| "The report concludes" | "We conclude" or "The team found" |
| "The strategy evolves" | "We shifted the strategy" |
| «Решение было принято» | «Мы решили» |

Exception: when the actor is genuinely unknown, irrelevant, or the passive serves a deliberate purpose (e.g. legal/contract language).

---

## 8. Trust the reader

Cut over-explanation:
- Don't justify every transition.
- Don't summarize what you just said.
- Don't preview what's coming ("In the rest of this section, we will…").
- Don't restate the obvious.

Real writing leaves room for the reader to connect dots.

---

## 9. Direct claims over hedging

Pick one qualifier max per claim. If you find "may possibly perhaps could potentially" — collapse to one or zero.

| Hedged | Direct |
|---|---|
| "This may potentially help with retention" | "This helps retention" or "Likely lifts retention" |
| "It could be argued that…" | "[Subject] argues…" or "I think…" |
| «Возможно, это может помочь» | «Это помогает» / «Скорее всего, это поможет» |

---

## 10. Avoid over-cleaning

Human ≠ messy. Don't:
- Inject typos or "lol" / «лол».
- Add slang that wasn't in the source register.
- Force casual tone into a B2B email.
- Break perfectly fine sentences just to add variation.

Human = intentional. Each sentence chosen, not formula-generated.

---

## 11. Keep what's specific

Names, numbers, dates, URLs, citations, technical terms, brand names — never alter. If the agent passes a `preserve` list, treat those tokens as immutable.

---

## 12. End on substance, not summary

Last line of the rewrite should be:
- a concrete claim, OR
- a next step / action, OR
- a sharp observation that lands without theatrics.

Not:
- "In conclusion…"
- "Ultimately…"
- "And that matters."
- A motivational close.

---

## 13. No theatrical reveal on the last line

If the last sentence of the rewrite is **shorter than the post's average sentence length** AND has the shape of a reveal — "It's the [adj] [noun].", "That's the [noun].", "This is the [noun].", «Это и есть [сущ.]» — rewrite it.

Two repair options:
- Merge it into the previous sentence so the reveal becomes a clause, not a drop-the-mic line.
- Replace the last sentence with a concrete claim or named action that doesn't perform "having a point."

Why: the substantive-reveal closer (TELL-016 Pattern B) is the most common AI tell that survives every other rewrite pass. It looks like content — it's actually theatre.

---

## 14. No arrow-flowchart compression

No `→` characters in prose output. No "X → Y → Z" sequences. No vertical stacks of one-word steps.

If the source uses arrows to compress a process, rewrite as a sentence with named actors and verbs. If the process can't be named in prose without going abstract, the arrow form was hiding emptiness — cut.

Exception: technical pipeline / system diagram / architecture description in actual technical docs.

---

## 15. Paragraph-rhythm variety in posts

For social posts (LinkedIn, Telegram channel, X, blog post — any `content_type` that publishes paragraphs separated by whitespace):

- At least one paragraph in the output must be 4+ sentences of continuous prose. Not setup→reveal. Real claim with reasoning, named example, or extended observation.
- At most ~50% of paragraphs may be the 1–2 sentence thrust shape.
- Mix sentence lengths *inside* paragraphs (5-word and 20-word in the same block).
- Don't put a blank line between every two-sentence claim.

Why: even when individual sentences pass every other check, a metronomic paragraph rhythm of `2-1-2-2-1-2` reads as AI/LinkedIn template at the structural level. Real human posts on the same topic look more like `5-1-3-6-2-4`.

---

## 16. No reframe couplets (second-person rebrand)

The shape "You're not just X anymore. You're Y." (TELL-022) almost never survives a real human edit. If the source has it:

- If the second sentence carries information the first doesn't, keep only the second (drop the negated framing).
- If both are framings of the same idea with no new fact, cut the whole couplet.
- For founder voice that wants to make a point: replace with a first-person claim with named specifics.

---

## Order of operations (cheat sheet)

```
FRAME TASK (register: said to one person; goal: be understood)
       → DETECT → CUT FILLER → REPLACE ABSTRACTIONS → FIX RHYTHM
       → REMOVE TRANSITIONS → KILL REFRAME COUPLETS → REWRITE ARROW STEPS
       → APPLY VOICE → CHECK PARAGRAPH-RHYTHM VARIETY
       → CHECK LAST LINE FOR THEATRICAL REVEAL
       → CHECK PRESERVE LIST → SCORE
```
