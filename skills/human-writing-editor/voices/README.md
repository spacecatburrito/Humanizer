# Voice Library

User-contributed voice references. Each subfolder = one voice.

When the skill is invoked with `voice=<folder-name>`, all samples plus `_profile.md` from that folder are loaded into the rewrite prompt.

---

## Layout

```
voices/
├── _template/                 ← starter for new voices, do not invoke
│   ├── _profile.md            ← style description (filled by build-profile)
│   └── sample-001.md          ← raw sample
│
├── my/                        ← reserved name for the user's own voice
│   ├── _profile.md
│   ├── sample-001.md
│   ├── sample-002.md
│   └── ...
│
├── denis-sexy/                ← admired author, kebab-case
│   ├── _profile.md
│   ├── sample-001.md
│   └── ...
│
└── <other-voice>/
```

Folder name rules:
- kebab-case, ASCII only
- `_template` and names starting with `_` are reserved, never invoked as a voice
- `my` is the conventional name for the user's own voice — used as the default for `voice=my`

---

## How to populate a voice (3 input methods)

### Method 1 — paste

User pastes text into chat. Claude saves it:

```
Save this as a sample for voice=my:

[pasted text]
```

Claude creates `voices/my/sample-NNN.md` with frontmatter (date, source=paste, language).

### Method 2 — URL

```
Add this as a sample for voice=denis-sexy:
https://t.me/denissexy/12345
```

Claude uses WebFetch to retrieve the content, strips boilerplate, saves text-only as `voices/denis-sexy/sample-NNN.md` with frontmatter (source=URL, retrieved date).

If the URL is a Telegram channel (`t.me/<channel>` or `t.me/<channel>/<msg>`), Claude tries the public web view first. If unavailable, asks user to paste instead.

### Method 3 — MD file on disk

```
Add /path/to/post.md as a sample for voice=my
```

Claude reads the file and copies content into a new sample file under `voices/my/`. Original file stays untouched.

---

## Sample file format

Each sample lives in its own file: `sample-001.md`, `sample-002.md`, etc.

Frontmatter:

```yaml
---
source: paste | url | file
source_url: <url if applicable>
source_path: <path if applicable>
collected: YYYY-MM-DD
language: en | ru | mixed
content_type: linkedin | telegram-channel | email | proposal | website | social-post | other
---

[raw text of the sample]
```

The text below frontmatter is the actual writing — preserved verbatim, no edits.

---

## `_profile.md` — style descriptor

After samples are collected, Claude runs the `build-profile` step (see SKILL.md) which writes `_profile.md` in the voice folder.

Profile contents (auto-generated, human-editable):

```markdown
---
voice: <name>
last_built: YYYY-MM-DD
sample_count: N
languages: [en, ru]
---

# Voice profile: <name>

## Sentence-length signature
- Average: X words
- Variance: high / medium / low
- Distribution: ~A% short (≤8w), ~B% medium (9–18w), ~C% long (19+ w)

## POV preference
- Pronouns: I / we / you / impersonal — relative frequencies
- First-person observation: yes / no
- Direct address to reader: yes / no

## Vocabulary register
- Formal score: 0.0–1.0
- Distinctive vocabulary: list of recurring words / phrases
- Avoided patterns: things this voice never does

## Punctuation habits
- Em dash usage: count per 100 words
- Parentheses: count per 100 words
- Setup colons: count per 100 words
- Bullet lists: yes / no, frequency
- Bold / italic: yes / no, what for

## Opening pattern
- declarative claim / question / scene / fact / observation / hook

## Closing pattern
- claim / action / observation / fragment / call-to-discussion

## Topical preferences
- list of recurring themes / domains

## Voice axes (estimated)
- Formal ↔ Casual: 0.0–1.0
- Soft ↔ Assertive: 0.0–1.0
- Abstract ↔ Concrete: 0.0–1.0
- Analytical ↔ Narrative: 0.0–1.0

## Quirks worth preserving
- specific habits, signature phrases, structural moves

## Anti-patterns
- things to NEVER copy from this voice (typos, off-brand jokes, dated references)
```

The profile is reference material. The samples are the ground truth — the LLM matches the writing to *them*, not to a description of them.

---

## How `voice=<name>` is resolved

1. Skill checks `voices/<name>/` exists and is not reserved (`_…`).
2. Loads all `sample-*.md` files (strips frontmatter, keeps body).
3. Loads `_profile.md` if present.
4. Prepends to the rewrite system prompt under section `=== voice-reference: <name> ===`.
5. Adds instruction: "Match the rhythm, vocabulary register, sentence-length distribution, POV, and punctuation habits of the samples below. Do not copy phrases or facts from them. Do not adopt the sample's specific topical content. The user's draft text is below."

If `<name>` doesn't exist, skill falls back to the closest base profile from `voice-profiles.md` and warns the user.

---

## Mixed-language voices

Voice samples can be RU, EN, or both. Profile records languages covered. When skill is invoked with `language=ru` and the matched voice has only EN samples (or vice versa), skill warns: "voice=<name> has no <language> samples; style transfer cross-language is approximate."

If the user wants strict separation, use suffixed folders: `my-ru/`, `my-en/`.

---

## Privacy / git

- `voices/` is part of the skill folder. Whatever the project's `.gitignore` policy is for `.claude/skills/` applies.
- Samples may contain personal data. Treat as private.
- For the consumer product (TG bot), voice samples are stored per-user in the product's own DB, not in this folder.
