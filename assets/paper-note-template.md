## Obsidian Paper Note Template

Fill every placeholder in CAPS. Keep the structure exactly — the frontmatter fields are chosen to work with Obsidian's Dataview plugin, so the user can later query "all unread high-relevance robotics papers" etc. Use `[[double brackets]]` for anything that should become a linked node in the graph (concepts, methods, authors, related papers). Use kebab/lowercase `#tags`.

For a multi-paper scan, also produce a separate **MOC note** (template at the bottom).

---

### Single-paper note

```markdown
---
title: "PAPER TITLE"
authors: [FIRST AUTHOR, ET AL]
year: YEAR
source: arXiv          # arXiv | bioRxiv | medRxiv | HuggingFace | journal
arxiv_id: "XXXX.XXXXX" # or doi: "..."
url: https://arxiv.org/abs/XXXX.XXXXX
published: YYYY-MM-DD
added: YYYY-MM-DD
status: unread         # unread | reading | read
relevance: high        # high | medium | low
rating:                # fill after reading, 1-5
tags: [paper, TOPIC-TAG, METHOD-TAG, to-read]
---

# PAPER TITLE

> [!tldr] Verdict
> ONE-TO-TWO SENTENCE VERDICT WITH A STANCE. What it is, whether it delivers, and the main caveat.

**Source:** [SOURCE] · **Published:** YYYY-MM-DD · **Status:** preprint / peer-reviewed
**Link:** URL

## Problem & contribution
- **Problem:** WHAT GAP IT TARGETS.
- **Claimed contribution:** THE ONE OR TWO NEW THINGS.

## Method
PLAIN-LANGUAGE DESCRIPTION of the approach — architecture, training signal, key trick. 2-4 sentences.

## Evidence
- **Datasets / setup:** ...
- **Baselines:** ...
- **Metrics / results:** ...
- **Real-robot vs sim / sample size:** ...

## Methodology critique
- **Holds up:** SPECIFIC STRENGTH.
- **Shaky:** SPECIFIC, SUBSTANTIATED WEAKNESS (eval gap, missing baseline, stats, reproducibility).

## Novelty vs prior work
Builds on [[PREDECESSOR 1]] and [[PREDECESSOR 2]]. WHERE IT SITS: new mechanism / known method new domain / scale result / incremental. Does it actually beat what it claims to?

## Relevance to my work
CONCRETE "SO WHAT FOR YOU" — a method to try, a baseline to beat, a dataset to use — linked to [[markerless motion capture]] / [[injury prediction]] / [[humanoid control]] / etc. Or an explicit "not relevant because…".

## Read next
- [[REFERENCE OR FOLLOW-ON 1]] — why.
- [[REFERENCE OR FOLLOW-ON 2]] — why.

## Notes
(Space for the user's own annotations.)
```

### MOC note (for multi-paper scans)

```markdown
---
title: "Research scan: TOPIC (YYYY-MM-DD)"
added: YYYY-MM-DD
tags: [moc, research-scan, TOPIC-TAG]
---

# Research scan: TOPIC

Window: LAST N MONTHS · Sources: arXiv / bioRxiv / HF · Scanned YYYY-MM-DD.

| Paper | Verdict | Relevance |
|---|---|---|
| [[PAPER 1 TITLE]] | ONE-LINE VERDICT | high/med/low |
| [[PAPER 2 TITLE]] | ONE-LINE VERDICT | high/med/low |

## Themes spotted
- CROSS-PAPER PATTERN OR TENSION worth noting.

## Skipped (and why)
- TITLE — reason (duplicate, survey, off-topic).
```

---

### Obsidian deep link

After saving each note, offer a deep link so the user can drop it into their vault in one click. Two options:

1. **Open an existing file** (if they save the `.md` into their vault folder first):
   `obsidian://open?vault=VAULT_NAME&file=FOLDER%2FNOTE_TITLE`

2. **Create a new note with the content inline** (good for short notes):
   `obsidian://new?vault=VAULT_NAME&name=NOTE_TITLE&content=URL_ENCODED_MARKDOWN`

Tell the user to replace `VAULT_NAME` with their actual vault. For long notes the URL gets unwieldy, so the downloaded `.md` file is usually cleaner — the deep link is a convenience, not the main delivery.
