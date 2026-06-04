# Human Writing Editor - getting started

A Claude Code skill that makes text sound like a real person wrote it. It detects AI tells (em-dash drama, tricolons, "It's not X, it's Y", motivational closers, corporate filler), rewrites for intent and rhythm, and can match a specific voice. Bilingual: English and Russian. It preserves facts, numbers, names, and citations.

This README is for someone receiving the skill and wanting to use it. The full rule set and internals live in [SKILL.md](SKILL.md).

> **Your own texts are optional.** On first run the skill asks once whether you want to teach it your voice (paste a few of your posts, or an author you like) - now or later. Say "later" and it works out of the box on a neutral-professional voice. You can add your texts anytime. See [section 5](#5-teach-it-your-voice-optional-but-powerful).

---

## 1. Install (one-click plugin)

You need [Claude Code](https://docs.anthropic.com/en/docs/claude-code) first:

```
npm install -g @anthropic-ai/claude-code
```

This skill ships as a Claude Code plugin. Inside Claude Code, add the marketplace and install:

```
/plugin marketplace add spacecatburrito/Humanizer
/plugin install humanizer@humanizer
```

No file copying. Update later with `/plugin update humanizer`.

> `spacecatburrito/Humanizer` is the GitHub repo this plugin lives in. If you are the one publishing it, see [PUBLISHING.md](PUBLISHING.md).

### Confirm it loaded

Start a new Claude Code session and run:

```
/human-writing-editor
```

If Claude lists it as an available skill, you are ready. The first time you actually use it, it asks once whether you want to load your own texts (see [section 5](#5-teach-it-your-voice-optional-but-powerful)).

---

## 2. The fastest way to use it

You do not need to remember any syntax. Paste your text and say what you want in plain language:

```
Humanize this, it sounds like ChatGPT wrote it:

[your draft]
```

```
Score how AI this reads, don't rewrite it yet:

[your draft]
```

Claude picks sensible defaults (rewrite mode, auto-detect language, standard strictness) and returns the result.

---

## 3. The four things it can do (modes)

Say the mode in words, or pass `mode=...`.

| Mode | Ask for it like this | You get back |
|---|---|---|
| `rewrite` (default) | "humanize / rewrite this" | only the rewritten text, no commentary |
| `check` | "check how AI this sounds" | a score plus the top issues and one-line fixes, no rewrite |
| `variants` | "give me a few versions" | three versions: clean-professional, operator-sharp, casual-direct |
| `score-only` | "just score it" | the numeric score block, for pipelines |

The score is AI-ness 0–10 across seven dimensions (lower is more human). 0 means it reads like a person; 10 means pure slop.

---

## 4. Tell it the format and how hard to cut (optional)

Both are inferred if you say nothing, but you can be explicit:

- **Content type:** `linkedin`, `email`, `telegram-dm`, `telegram-channel`, `proposal`, `website`, `social-post`, `academic`, `general`. Each has format-specific rules.
- **Strictness:** `light` (touch only the worst tells), `standard` (default), `aggressive` (rewrite freely, restructure, drop dead sentences - use on heavy AI slop).
- **Preserve list:** names, numbers, claims, dates, URLs that must not change. Example: `preserve: "Lucas, 9.4%, June 2026"`.

Example with everything spelled out:

```
Rewrite this as a telegram-channel post, aggressive strictness,
preserve the numbers and the product name:

[your draft]
```

---

## 5. Teach it your voice (optional but powerful)

By default it uses one of six base voices (`operator`, `founder`, `creator`, `neutral-pro`, `analyst`, `casual`). You can also build a custom voice from real samples of how you (or an author you admire) write.

On your very first run the skill asks once whether you want to do this now or later, so you do not have to find this section yourself. Either answer is fine - "later" just keeps the neutral default, and you can come back anytime with the steps below.

**Add samples** - paste, a URL, or a file on disk:

```
Save this as a sample for voice=my:

[paste a post you wrote]
```

```
Add this as a sample for voice=my:
https://t.me/yourchannel/123
```

**Build the profile** once you have three or more samples:

```
/human-writing-editor build-profile my
```

**Use the voice** on any future rewrite:

```
Humanize this in voice=my:

[your draft]
```

The samples are the ground truth - the rewrite matches their rhythm, vocabulary, and sentence-length, without copying their words or topics. Full details and the voice-library commands (`list-voices`, `delete-voice`, etc.) are in [voices/README.md](voices/README.md) and [SKILL.md](SKILL.md).

---

## 6. What it will not do

- It does not add typos, slang, or fake casualness to seem human.
- It does not change facts, numbers, names, dates, or URLs.
- It is not an AI-detector bypasser. The goal is human *reading*, not passing a detector.
- It is not a translator. Russian stays Russian, English stays English.
- It is not a fact-checker. It preserves what your draft claims; truth is on you.
- It never outputs em dashes (—). If a dash is unavoidable it uses a spaced hyphen ( - ).

---

## 7. Calling it from other agents

If you build writing agents (post generators, proposal drafts), have them call this skill as a final pass:

```
mode=rewrite
voice=<your house voice>
content_type=<format>
preserve=<facts/numbers/names from the source>
```

Always pass `preserve` - the rewrite is aggressive on filler but must never touch protected content. See the "Composing from other agents" section in [SKILL.md](SKILL.md).
