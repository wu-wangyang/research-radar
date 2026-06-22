---
name: research-radar
description: Find and analyze the latest research papers in ML/AI, robotics, and sports science, then produce an Obsidian-ready note with methodology critique, novelty assessment, relevance to the user's work, and a concrete reading plan. Use this whenever the user asks what is new/latest/recent in a research area, wants a paper or preprint reviewed, summarized, or critiqued, asks to track a topic or author, mentions arXiv, bioRxiv, or Hugging Face papers, or wants research notes for their Obsidian vault — even if they never say the word "skill". Bias hard toward the newest preprints, verify recency, and never just restate the abstract.
---

# Research Radar

Find the freshest, most relevant papers in ML/AI, robotics, and sports science, then turn each one into a sharp, opinionated note that lands in the user's Obsidian vault as a connected piece of their knowledge graph.

The whole point is to save the user reading time *without* dumbing things down. A note that just paraphrases the abstract is a failure — they could read the abstract themselves in 20 seconds. The value is in the judgment: is this real or hype, how does it relate to what came before, does it matter for *their* work, and what should they read next.

## When to use this

Trigger on any of: "what's new in X", "latest papers on Y", "any recent work on Z", "review this paper / preprint", "summarize this arXiv link", "track [topic/author]", "make me a research note", or a dropped arXiv/bioRxiv/HF URL. Also trigger proactively when the user is clearly doing a literature scan even if phrased casually.

## Workflow

Follow these steps in order. Don't skip the analysis depth to save time — depth is the product.

### 1. Pin down scope (briefly)

Infer as much as possible before asking. You usually need: the **topic** (and any must-have subtopics), the **time window** (default: last 3 months; "latest" means newest-first), **how many papers** (default: 3–5 for a scan, 1 for a deep review), and **depth** (scan digest vs. deep single-paper review). Only ask if a choice genuinely changes the output and you can't infer it.

If the user dropped a specific paper/URL, skip straight to step 4 for that paper.

### 2. Search the right sources

Route by subtopic — see `references/source-routing.md` for exact query syntax, categories, and the arXiv API call. Quick map:

- **ML/AI methods, RL, vision, learning-based control** → arXiv (`cs.LG`, `cs.AI`, `cs.RO`, `cs.CV`, `stat.ML`), sorted by submission date; cross-check Hugging Face Papers for what's trending.
- **Humanoid / legged robot control, sim-to-real, motion** → arXiv `cs.RO` + the `awesome-humanoid-robot-learning`-style lineage; HF Papers.
- **Biomechanics, markerless motion capture, sports science, injury modeling** → bioRxiv (via the bioRxiv connector) + arXiv `cs.CV`/`eess.IV` for the vision side.
- **Models / datasets / benchmarks** → Hugging Face (connector or huggingface.co).

"Most up to date" is a hard requirement: sort by date, prefer the newest, and **state each paper's date and preprint-vs-published status**. If a connector for a source isn't available, fall back to `web_search` + `web_fetch` on the source's site and say so.

### 3. Triage and select

From the raw hits, pick the ones worth a full note. Drop near-duplicates (same group's incremental v2), deprioritize pure surveys unless the user wants a landscape, and flag when a preprint already has a peer-reviewed version (link the better one). For each candidate, do a quick relevance gut-check against the user's interests before committing to a full analysis. Tell the user what you selected and what you skipped, in one line each.

### 4. Analyze each paper — the core

This is where the skill earns its keep. Read `references/analysis-rubric.md` and apply all four insight layers to every paper:

1. **Methodology critique** — what's actually solid vs. shaky (eval gaps, missing baselines, weak stats, tiny n, cherry-picked benchmarks, no code/reproducibility).
2. **Novelty vs prior work** — genuinely new or incremental? What lineage does it extend? Name the predecessors.
3. **Relevance to the user's work** — markerless mocap, ML injury prediction, humanoid/legged control, clinical data systems. Be concrete about *how* they'd use it, or say plainly if it's not relevant.
4. **What to read next** — the 1–2 references or follow-ons that matter most.

Pull the real content (don't analyze from the abstract alone): use `web_fetch` on the arXiv abstract/HTML page or PDF, or `get_preprint`/`get_full_text_article` from the connectors. Respect copyright: paraphrase; any direct quote stays under 15 words with attribution, one per source max.

### 5. Write the Obsidian note

Use `assets/paper-note-template.md` exactly. Each note must have: YAML frontmatter (Dataview-friendly fields), `#tags`, and `[[wikilinks]]` connecting the paper to concepts, methods, authors, and related papers so it wires into the user's graph. For a multi-paper scan, also write one **MOC (map-of-content) note** that links to each paper note with a one-line verdict.

Save notes as `.md` files in the outputs directory, then present them. Also generate an `obsidian://new` deep link per note (see template footer) so the user can drop it straight into their vault — note that the vault name is theirs to fill in, and that for long notes the downloaded `.md` file is the cleaner path.

## Quality bar (read before finishing)

A note passes only if a knowledgeable reader would learn something they couldn't get from the abstract. Concretely:
- The TL;DR states a **verdict**, not a topic ("Solid sim-to-real gain but eval is single-environment" — not "A paper about humanoid locomotion").
- At least **one specific, substantiated critique** per paper. "Looks good" is not a critique.
- The relevance section says *how the user would use it*, or explicitly "not relevant to your current work because…".
- Novelty names at least one **predecessor** it builds on or beats.
- No abstract-restatement, no hype-laundering ("revolutionary", "groundbreaking") unless you're quoting and flagging it.

If you can't meet the bar for a paper (e.g. can't access the content), say so rather than padding.
