---
name: human-writing-editor
description: Detects AI-sounding patterns in prose and rewrites text into sharper, human, context-aware language while preserving meaning and facts. Use whenever drafting, editing, post-processing, or scoring writing — LinkedIn posts, emails, Telegram messages, channel posts, proposals, landing copy, decks, social media, academic prose. Bilingual (EN + RU). Composable: callable from other agents and skills, and packageable as the prompt core of the consumer humanizer product.
version: 0.4.0
---

# Human Writing Editor

The job: make text sound like a real person wrote it. Not because of typos or fake casualness — because of intent, specificity, rhythm, and voice.

This skill is the single source of humanization rules used across:
1. Internal writing tasks (post-writer, tss-post-writer, contract drafts, landing copy).
2. The consumer humanizer product (Telegram bot, future web/extension).

Same files. Same rules. The product wraps this skill; agents call it.

## When to invoke

Trigger on any of:
- "humanize", "remove AI tone", "make it sound human", "less GPT-ish"
- editing AI drafts before publishing
- pre-flight pass on text written by another agent
- "check AI-ness", "score this text"
- "rewrite in my voice", "make it sharper", "more direct"

## Inputs

| Field | Values | Default | Notes |
|---|---|---|---|
| `text` | string | required | source draft |
| `language` | `en` \| `ru` \| `auto` | `auto` | infer if not set |
| `mode` | `check` \| `rewrite` \| `variants` \| `score-only` | `rewrite` | output shape |
| `content_type` | `linkedin` \| `email` \| `telegram-dm` \| `telegram-channel` \| `proposal` \| `website` \| `social-post` \| `academic` \| `general` | `general` | format-specific rules |
| `voice` | base profile (`operator` \| `founder` \| `creator` \| `neutral-pro` \| `analyst` \| `casual`) **or** custom voice folder name from [voices/](voices/) (e.g. `my`, `denis-sexy`) | `operator` | base profiles in [references/voice-profiles.md](references/voice-profiles.md); custom voices in [voices/README.md](voices/README.md) |
| `strictness` | `light` \| `standard` \| `aggressive` | `standard` | how hard to cut |
| `preserve` | list of strings | `[]` | names, numbers, claims, citations that must not change |

If invoked from chat without explicit fields, infer reasonable defaults from context.

## First-run onboarding (voice offer)

The first time a real user invokes the skill interactively, offer to teach it their voice - before doing anything else. The point: the user learns the option exists up front, without reading the README.

**When to offer (all must hold):**
- The invocation is interactive (a person in chat), NOT composed from another agent. If the call carries explicit fields like `preserve`, or comes from post-writer / tss-post-writer / any agent pipeline, skip the offer entirely.
- No custom voice exists yet: `voices/` contains only reserved folders (`_*`).
- The onboarding marker `voices/.onboarded` does not exist.

**What to ask (once):**

> Before I rewrite - want me to match a specific voice? You can paste a few of your own posts (or an author you like) so I copy your tone of voice. This is optional: skip it and I'll use a clean neutral-professional voice. You can add your texts anytime later.
>
> 1. Load my texts now - paste / URL / file path
> 2. Skip for now, just humanize (I can learn my voice later)

- If the user chooses **now**: run the `add-voice` flow (default `voice=my` unless they name another), collect samples, and once there are ≥3 run `build-profile`. Then proceed with the rewrite using that voice.
- If the user chooses **later** (or ignores and just wants the text done): proceed with the default base voice. Do not ask again.

**After the offer (either choice), write `voices/.onboarded`** (a one-line stamp: `offered: <today>`) so the skill never re-asks. Adding a voice later via `add-voice` works exactly the same regardless of this marker.

Do not block on this offer if the user clearly already gave a `voice=` argument - they know about it; just honor it and stamp `.onboarded`.

## Three-layer model

1. **Detect** — scan input for AI markers. Rules: [references/ai-tells.md](references/ai-tells.md).
2. **Rewrite** — apply [references/rewrite-principles.md](references/rewrite-principles.md) + [references/content-modes.md](references/content-modes.md) for the chosen `content_type`.
3. **Voice** — resolve `voice`:
   - if `voice` matches a base profile in [references/voice-profiles.md](references/voice-profiles.md), apply it
   - if `voice` matches a folder in [voices/](voices/) (excluding names starting with `_`), load that folder's samples and `_profile.md` (see [voices/README.md](voices/README.md))
   - if not found, fall back to `operator` and warn
   - For RU, also load [references/ru-specific.md](references/ru-specific.md).

## Process

### 1. Load references

Always: ai-tells.md, rewrite-principles.md, aliveness.md, content-modes.md (filter to `content_type`), voice-profiles.md (filter to `voice`).
If `language=ru` (or auto-detect=ru): also ru-specific.md.

### 2. Detect

Build an issue list. Each issue: `tell_id` (e.g. `TELL-002`), excerpt, why it reads as AI, fix direction.

### 3. Rewrite — apply this order

1. Cut filler (corporate padding, generic openers, forced conclusions, importance phrases, adverbs).
2. Replace abstractions with concrete nouns / numbers / actions.
3. Break predictable rhythm — vary sentence length, drop symmetric structures, kill rule-of-three when artificial.
4. Remove default transitions (However, Moreover, Additionally; «однако», «более того», «кроме того») — restructure or use direct continuation.
5. Apply voice profile: tone, sharpness, point-of-view, sentence-length distribution.
6. Run the aliveness pass ([references/aliveness.md](references/aliveness.md)): check for BEIGE-001…005, apply the techniques, voice-gated. Cutting slop is not the finish line; the output must read like the author on a good day, not like a sanitized report.
7. Re-read against `preserve` list — verify nothing protected was dropped or altered.

### 4. Hard rules (never violate)

- Do NOT add typos, slang, or fake casualness.
- Do NOT change names, numbers, claims, citations, dates, URLs.
- Do NOT optimize for AI detectors. Optimize for human reading. The metric is: would a real person write this.
- Do NOT use em dashes (—) as default rhythm devices. Period or comma instead.
- Do NOT use "It's not X, it's Y" / "это не про X, это про Y" contrast formulas.
- Do NOT use the "no X, no Y, no Z — just W" triple-negation formula (TELL-024).
- Do NOT close a line with a standalone "By design." / "On purpose." / "Deliberately." tag (TELL-025).
- Do NOT use "X is the headline" / "the real story is X" framing-about-framing (TELL-026).
- Do NOT add "Let that sink in", "The truth is", "Here's the thing", «Скажу честно», «Дело вот в чём».
- Do NOT inject motivational/inspirational closers.

### 5. Score

Compute AI-ness 0–10 using [references/scoring.md](references/scoring.md). Report sub-scores per dimension.

### 6. Output

Format by mode:

- **`check`** — diagnosis only: AI-ness score, sub-scores, top 3–5 issues with excerpts, one-line fix per issue. No rewrite.
- **`rewrite`** — only the rewritten text. No commentary, no diff, no preface.
- **`variants`** — three versions: *clean-professional*, *operator-sharp*, *casual-direct*. No commentary between them.
- **`score-only`** — score block only (for eval pipelines).

## Sub-commands (voice library management)

In addition to rewrite/check/variants/score, the skill exposes voice-library management. Trigger by user-language matches like below; all create/modify files under [voices/](voices/).

### `add-voice <name>` — add a sample to a voice

Triggers on phrases like:
- "save this as a sample for voice=<name>" / "сохрани как образец для голоса <name>"
- "add this post to voice <name> reference" / "добавь пост в референс <name>"
- "add this URL as <name> sample" / «добавь эту ссылку в <name>»

**Three input methods (auto-detected):**

1. **Paste** — user pastes raw text in the message. Save as `voices/<name>/sample-NNN.md` with frontmatter (`source: paste`, `collected: <today>`, `language: <auto>`, `content_type: <ask if unclear>`). NNN = next available zero-padded index.
2. **URL** — user provides a URL. Use WebFetch to retrieve, extract the article/post body (strip nav, ads, comments), save as `sample-NNN.md` with `source: url, source_url: <url>`. If the URL is a Telegram channel post (`t.me/...`) and WebFetch fails, ask user to paste instead.
3. **File path** — user provides path to an `.md` or `.txt` file on disk. Read with the Read tool, copy body content (strip frontmatter if any) into `sample-NNN.md` with `source: file, source_path: <path>`.

If `voices/<name>/` doesn't exist yet, create it. Never overwrite existing samples.

After save, report: `Added sample-NNN to voices/<name>/. Run /human-writing-editor build-profile <name> when you have ≥3 samples to refresh the style profile.`

### `build-profile <name>` — analyze samples, write `_profile.md`

Read all `sample-*.md` files in `voices/<name>/`. Compute / estimate:
- Average sentence length and variance.
- Sentence-length distribution (% short / medium / long).
- Pronoun frequencies and POV preference.
- Vocabulary register score (0–1).
- Distinctive words / phrases that recur across samples.
- Punctuation habits (em dash, parentheses, setup colons per 100 words).
- Opening pattern (first line of each sample).
- Closing pattern (last line of each sample).
- Topical preferences.
- Voice axes coordinates (Formal↔Casual, Soft↔Assertive, Abstract↔Concrete, Analytical↔Narrative).
- Quirks worth preserving + anti-patterns.
- Suggest the closest base profile (operator/founder/creator/neutral-pro/analyst/casual).

Write to `voices/<name>/_profile.md` using the template at [voices/_template/_profile.md](voices/_template/_profile.md). Update frontmatter `last_built` and `sample_count`.

If sample count is <3, still write the profile but mark `confidence: low` and recommend more samples.

### `list-voices` — show available custom voices

List subfolders of [voices/](voices/) (excluding `_*`). For each, show: sample count, languages covered, last_built date from `_profile.md`, suggested base profile.

### `delete-voice <name>` — remove a voice folder

Confirm with user first. Then `rm -r voices/<name>/`. Reserved names (`_*`) cannot be deleted.

### `delete-sample <name> <NNN>` — remove a single sample

Delete `voices/<name>/sample-NNN.md`. Suggest rebuilding the profile after.

---

## Composing from other agents

Pattern for any writing agent (post-writer, tss-post-writer, contract drafts):

```
1. Agent drafts content per its own template / few-shot examples.
2. Agent invokes human-writing-editor with:
     mode=rewrite
     voice=<agent's house voice>
     content_type=<format>
     preserve=<facts/numbers/names from source>
3. Agent returns the rewritten output.
```

Agents must pass `preserve` — humanizer is aggressive on filler but should never touch protected content.

## Product packaging

For the consumer humanizer (Telegram bot etc.), bundle the same reference files into the LLM system prompt. Recipe and bundling logic: [product-bundle.md](product-bundle.md).

## Bilingual rules

- Rewrite in the source language. Never translate-to-rewrite-then-translate-back.
- RU has its own tells (calques from EN, verb-noun bloat «осуществлять выполнение», participial chains, «является», «позволяет», «данный»). See [references/ru-specific.md](references/ru-specific.md).
- Voice profiles work in both languages with deltas noted in ru-specific.md.

## Strictness calibration

| Level | What it does |
|---|---|
| `light` | Fix only highest-confidence AI tells. Preserve original wording where possible. Use when the draft is mostly fine and the user wants minimal changes. |
| `standard` | Default. Cut filler, replace abstractions, fix rhythm, apply voice. |
| `aggressive` | Rewrite freely. Restructure paragraphs. Drop sentences that add nothing. Use when source is heavy AI slop. |

## What this skill is NOT

- Not a paraphraser. Replacing words alone produces worse AI text.
- Not an AI-detector bypasser. The promise is human reading, not detector pass.
- Not a translator. RU stays RU, EN stays EN.
- Not a fact-checker. It preserves what the source claims; agents are responsible for source truth.
