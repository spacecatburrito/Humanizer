# Humanizer

A Claude Code plugin that makes text sound like a real person wrote it. It detects AI tells (em-dash drama, tricolons, "It's not X, it's Y", motivational closers, corporate filler), rewrites for intent and rhythm, and can match a specific voice. Bilingual: English and Russian. It preserves facts, numbers, names, and citations.

The skill itself lives in [skills/human-writing-editor/](skills/human-writing-editor/) - see its [README](skills/human-writing-editor/README.md) for full usage.

## Install

You need [Claude Code](https://docs.anthropic.com/en/docs/claude-code) first:

```
npm install -g @anthropic-ai/claude-code
```

Then, inside Claude Code:

```
/plugin marketplace add spacecatburrito/Humanizer
/plugin install humanizer@humanizer
```

Confirm it loaded:

```
/human-writing-editor
```

Update later with `/plugin update humanizer`.

## Use it

Just paste your text and say what you want:

```
Humanize this, it sounds like ChatGPT wrote it:

[your draft]
```

Modes: rewrite (default), check (score + issues, no rewrite), variants (three versions), score-only.

Your own texts are optional. On first run the plugin asks once whether you want to teach it your voice (paste a few of your posts, or an author you like) - now or later. Say "later" and it works out of the box.

Full reference: [skills/human-writing-editor/README.md](skills/human-writing-editor/README.md).
