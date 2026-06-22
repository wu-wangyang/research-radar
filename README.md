# research-radar

A [Claude Skill](https://docs.claude.com) that finds the freshest, most relevant papers in **ML/AI, robotics, and sports science**, then writes each one up as an **Obsidian-ready note** — with methodology critique, novelty assessment, relevance to your own work, and a concrete reading plan.

The point is judgment, not summarization: a note that just paraphrases the abstract is treated as a failure. Every note has to earn its place with a verdict, a substantiated critique, and a "so what for you".

## What it does

- **Searches the right source per topic** — arXiv (`cs.LG`/`cs.RO`/`cs.CV`…) for ML and robotics, bioRxiv for biomechanics, Hugging Face Papers for what's trending — always biased toward the newest preprints, with recency verified.
- **Analyzes across four layers** — methodology critique, novelty vs prior work, relevance to your work, what to read next.
- **Outputs an Obsidian note** — Dataview-friendly frontmatter, `#tags`, `[[wikilinks]]` to wire papers into your graph, a `> [!tldr]` verdict callout, a map-of-content note for multi-paper scans, and an `obsidian://` deep link.

## Repo layout

```
research-radar/
├── SKILL.md                        # workflow + triggering + quality bar
├── references/
│   ├── source-routing.md           # arXiv API / bioRxiv / HF query syntax
│   └── analysis-rubric.md          # the four insight layers + worked example
└── assets/
    └── paper-note-template.md      # Obsidian note + MOC templates
```

The repo root *is* the skill folder — `SKILL.md` lives at the top level, so the installed skill's identity is the folder name `research-radar`.

## Build the installable `.skill`

A `.skill` file is just a zip with the skill folder at its root. Build one straight from the repo with `git archive` (this respects `.gitattributes`, so repo-meta files like this README are excluded from the package and `.git` never gets bundled):

```bash
git archive --format=zip --prefix=research-radar/ -o research-radar.skill HEAD
```

## Install

In Claude (claude.ai or the desktop/mobile app): **Settings → Capabilities/Skills → upload** `research-radar.skill`. Once installed it triggers automatically on prompts like "what's new in humanoid control", "review this arXiv link", or "make me a research note".

## Editing and iterating

Edit `SKILL.md`, `references/`, or `assets/` directly, commit, rebuild the `.skill`, and re-upload. Keep `SKILL.md` lean — detailed query syntax and the analysis rubric live in `references/` and load on demand. The Anthropic `skill-creator` tooling can validate the folder (`quick_validate.py`) and run eval loops if you want to test changes systematically.

## Notes

- The skill leans on the **bioRxiv** and **Hugging Face** connectors plus web access for arXiv; if a connector is off in a given chat it falls back to web search and says so.
- This repo is skill **source**. Output notes belong in your Obsidian **vault**, which should be its own repo if you version it.
