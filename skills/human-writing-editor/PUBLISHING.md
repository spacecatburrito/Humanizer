# Publishing as a Claude Code plugin

This turns the `human-writing-editor` skill into a one-click installable plugin. Users then run two commands and they're done - no folder copying.

You do this once, when you push to a public GitHub repo. After that, users install with:

```
/plugin marketplace add spacecatburrito/Humanizer
/plugin install humanizer@humanizer
```

(`humanizer@humanizer` = `<plugin-name>@<marketplace-name>`; both are named `humanizer` below.)

---

## Target repo layout

Create a **new, standalone public GitHub repo** with this structure. The skill lives under `skills/`, and two small manifest files make it a plugin marketplace:

```
<repo root>/
├── .claude-plugin/
│   ├── marketplace.json        ← lists the plugin (file 1 below)
│   └── plugin.json             ← describes the plugin (file 2 below)
├── skills/
│   └── human-writing-editor/   ← copy this whole folder here, unchanged
│       ├── SKILL.md
│       ├── README.md
│       ├── PUBLISHING.md
│       ├── references/
│       └── voices/
└── README.md                   ← optional; can be a copy of the skill README
```

Key point: Claude Code auto-discovers skills inside a plugin's `skills/` directory, so the folder name and the `references/` + `voices/` subfolders must stay intact.

---

## File 1 - `.claude-plugin/marketplace.json`

```json
{
  "name": "humanizer",
  "owner": {
    "name": "Elena",
    "url": "https://github.com/spacecatburrito"
  },
  "metadata": {
    "description": "Human Writing Editor - make text sound like a person wrote it."
  },
  "plugins": [
    {
      "name": "humanizer",
      "source": "./",
      "version": "1.0.0",
      "description": "Detects AI tells and rewrites prose for voice, rhythm, and intent. Bilingual EN + RU. Optional custom voice library."
    }
  ]
}
```

`"source": "./"` means the plugin is the repo root itself.

---

## File 2 - `.claude-plugin/plugin.json`

```json
{
  "name": "humanizer",
  "version": "1.0.0",
  "description": "Detects AI tells and rewrites prose for voice, rhythm, and intent. Bilingual EN + RU.",
  "author": {
    "name": "Elena"
  }
}
```

---

## Steps

```
# 1. Make the new repo folder
mkdir humanizer-plugin && cd humanizer-plugin
git init

# 2. Drop in the skill
mkdir -p skills
cp -R "/path/to/human-writing-editor" skills/

# 3. Add the two manifest files
mkdir -p .claude-plugin
#   create .claude-plugin/marketplace.json  (File 1 above)
#   create .claude-plugin/plugin.json       (File 2 above)
#   (<owner> is already set to spacecatburrito)

# 4. Commit and push to a PUBLIC GitHub repo
git add .
git commit -m "humanizer plugin v1.0.0"
git branch -M main
git remote add origin https://github.com/spacecatburrito/Humanizer.git
git push -u origin main
```

The repo must be **public** (or the user needs read access) - `/plugin marketplace add` clones it.

---

## What the user (e.g. Lucas) then does

1. Install Claude Code: `npm install -g @anthropic-ai/claude-code`
2. In Claude Code:
   ```
   /plugin marketplace add spacecatburrito/Humanizer
   /plugin install humanizer@humanizer
   ```
3. Confirm: `/human-writing-editor`. On first use it offers to load his own texts (optional).

---

## Updating later

Bump `version` in both manifest files, commit, push. Users update with:

```
/plugin update humanizer
```

---

## Privacy check before pushing

The repo is public. Before `git push`, confirm `skills/human-writing-editor/voices/` contains **only** the `_template/` folder - no real voice samples (those can hold personal writing). Custom voices live on each user's own machine, not in the published plugin.
