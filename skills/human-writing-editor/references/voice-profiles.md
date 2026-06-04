# Voice Profiles

Pluggable voices. Each profile = a calibration on four axes plus do/don't lists.

The four axes (use to fine-tune any profile):
- **Formal ↔ Casual** — vocabulary register
- **Soft ↔ Assertive** — strength of claims
- **Abstract ↔ Concrete** — level of specificity
- **Analytical ↔ Narrative** — argument vs. story

---

## `operator` (default)

**Position on axes:** Mid-formal · Assertive · Concrete · Analytical-leaning.

**Characteristics:**
- Direct. Commercially aware. Skeptical of fluff.
- Focused on outcomes, not process.
- Uses numbers and specifics.
- Mixes short and medium sentences. Occasional longer one for nuance.

**Do:**
- State the actual claim first.
- Use industry-standard precise terms (CAC, retention, churn, ARPU) without explaining unless audience requires it.
- Push back on hand-wavy framings.

**Avoid:**
- Motivational tone.
- Inspirational closures.
- Agency / consulting "deck-speak".
- Cute fragments.

**RU note:** Avoid «является», «осуществляет», «позволяет» (TELL-CORPRU-001). Prefer plain verbs: «делает», «работает», «решает».

---

## `founder`

**Position:** Mid-formal · Assertive · Concrete · Narrative-leaning.

**Characteristics:**
- Operator + first-person + opinion.
- Personal observations from running things.
- Willing to take a side.
- Shows reasoning, not just conclusions.

**Do:**
- Write "I" / «я». Own the claim.
- Reference specific decisions, lessons, mistakes.
- One strong opinion per piece.

**Avoid:**
- Influencer cadence ("Here's the truth: …").
- Performative humility ("I'm just learning…").
- Fake vulnerability.
- Lessons that sound copy-pasted from a self-help book.

---

## `creator`

**Position:** Casual · Mid-soft → Assertive · Mid-concrete · Narrative.

**Characteristics:**
- Conversational. Personal observations. Mild self-awareness.
- Suited to social posts (Telegram channel, LinkedIn personal, X).
- Willing to be funny. Willing to be wrong out loud.

**Do:**
- Use first person.
- Drop into informal register where it fits ("yeah", "ok", «ну», «короче» — sparingly).
- Reference real situations.
- Allow imperfection — partial thought, half-finished joke if it lands.

**Avoid:**
- Forced casualness ("lol", "tbh", «лол») unless source already has it.
- Setup-payoff colon hooks ("Here's what nobody tells you:").
- Three-fragment finishers.
- Motivational closes.

---

## `neutral-pro`

**Position:** Formal · Mid-soft · Mid-abstract · Analytical.

**Characteristics:**
- Clean professional register. Low personality.
- For B2B emails, contracts, formal proposals, support copy.
- Polite without padding. Clear without sharpness.

**Do:**
- State purpose in line one.
- Use precise terms.
- Keep paragraphs short.

**Avoid:**
- Personal opinion.
- Irony.
- First-person plural with vague "we" — name the team / company explicitly when it matters.
- Polite padding (TELL-008) — politeness ≠ padding.

---

## `analyst`

**Position:** Formal · Mid-assertive · Concrete · Strongly analytical.

**Characteristics:**
- Evidence-driven. Measured.
- Longer sentences allowed when the argument needs them.
- Uses qualifiers honestly (not as filler).
- Numbers carry the argument.

**Do:**
- Show the source / data.
- Distinguish observation from inference explicitly.
- Use one qualifier when uncertainty is real.

**Avoid:**
- Bold marketing claims.
- Personal voice.
- Provocations.

---

## `casual`

**Position:** Strongly casual · Mid-assertive · Concrete · Narrative.

**Characteristics:**
- DM / chat / Telegram personal message.
- Short. Decisive. Minimal structure.
- One clear ask or point per message.

**Do:**
- Cut greetings beyond a one-word hi.
- State the ask in line one or two.
- Lower-case is fine.
- Skip closings ("Best regards") — name only or nothing.

**Avoid:**
- Long setup.
- Polished paragraphs.
- Em dashes.
- Compound sentences with subclauses.

---

## Voice axis tuning

If user supplies axis values directly (e.g. `formal=0.3, assertive=0.8`), apply them on top of the chosen base profile. Treat as deltas, not overrides.

Coordinate cheat sheet:

| Axis | 0.0 | 0.5 | 1.0 |
|---|---|---|---|
| Formal | LinkedIn DM | LinkedIn post | Contract |
| Assertive | Tentative observation | Direct statement | Strong claim with stake |
| Concrete | "We help X" | "We help X do Y" | "We help X cut Y from 5d to 1d" |
| Analytical | Story-led | Story+claim | Argument-first |

---

## Detecting voice from a sample

If user passes a writing sample (their own past text), extract:
- Average sentence length and variance
- Pronoun preference (I / we / you / impersonal)
- Vocabulary register (formal score: count of formal words / total)
- Use of numbers and named entities
- Punctuation habits (em dash usage, parentheses, bullets)
- Opening pattern (declarative, question, scene, claim)
- Closing pattern (claim, action, observation, fragment)

Match the rewrite to those signals.

---

## Custom voices (voice library)

Beyond the six base profiles above, the skill loads custom voices from [voices/](../voices/). Each subfolder = one voice. Examples: `my` (the user's own writing), `denis-sexy` (admired author), etc.

When `voice=<name>` matches a folder in `voices/`:

1. **Load all sample files** from `voices/<name>/sample-*.md` (strip frontmatter, keep body).
2. **Load `_profile.md`** if present — it gives shorthand description of the style.
3. **Inject into system prompt** under section `=== voice-reference: <name> ===` with this instruction:

> Match the rhythm, vocabulary register, sentence-length distribution, POV, and punctuation habits of the samples below. Do not copy phrases or facts from them. Do not adopt the sample's specific topical content.

4. **Use the profile's `base_profile`** field as the fallback baseline (e.g. if profile says `base_profile: founder`, apply founder rules first, then layer on the sample-specific signals).

### Priority of signals when conflicting

Samples > `_profile.md` > base profile.

If samples and profile disagree, samples win — they're ground truth, profile is a description that may be stale.

### Cross-language transfer

Voice samples can be RU-only, EN-only, or mixed.

- Same-language rewrite (samples and target both RU, or both EN): full style transfer.
- Cross-language rewrite (samples RU, target EN, or vice versa): partial — sentence-length signature and punctuation habits transfer reliably; specific vocabulary and idioms don't. Skill should warn the user.
- For strict separation, store as language-suffixed folders: `my-ru/`, `my-en/`.

### When to refresh

Profile is rebuilt on demand (`build-profile <name>`). Recommend refreshing after:
- Adding ≥3 new samples.
- A noticeable shift in the user's style.
- Quarterly, if voice is in active use.

### `voice=my` is the convention

Reserve `voices/my/` for the current user's own writing. When user says "rewrite in my voice", "in my style", "сохрани мой стиль" — resolve to `voice=my`.

If `voices/my/` doesn't exist yet, suggest: "I don't have your voice samples yet — paste 3–5 of your past posts/messages and I'll set up `voice=my`."
