# Source Routing

How to query each source for the newest, most relevant work. Always sort by date and prefer the freshest results.

## arXiv (primary for ML/AI, robotics, vision)

Use the public API via `web_fetch`. It returns Atom XML — parse the `entry` elements (title, summary, authors, published, id, links).

**API call shape:**
```
http://export.arxiv.org/api/query?search_query=SEARCH&sortBy=submittedDate&sortOrder=descending&max_results=25
```

`SEARCH` syntax (combine with `+AND+`, `+OR+`):
- Category: `cat:cs.RO` (robotics), `cat:cs.LG` (ML), `cat:cs.AI`, `cat:cs.CV` (vision), `cat:stat.ML`, `cat:eess.IV`, `cat:cs.NE`.
- Keyword in title: `ti:humanoid`; in abstract: `abs:"motion capture"`; anywhere: `all:diffusion+policy`.
- Example — newest humanoid-control work: `cat:cs.RO+AND+all:humanoid`
- Example — markerless mocap: `cat:cs.CV+AND+abs:markerless+AND+abs:motion`
- Example — RL locomotion: `cat:cs.RO+AND+all:%22sim-to-real%22`

URL-encode quotes as `%22` and spaces as `+`. If the API is slow or blocked, fall back to fetching the listing page `https://arxiv.org/list/cs.RO/recent` and the abstract pages directly.

To read a paper: fetch `https://arxiv.org/abs/ARXIV_ID` for the abstract page, or `https://arxiv.org/pdf/ARXIV_ID` for the PDF. The HTML version at `https://arxiv.org/html/ARXIV_ID` (when present) is easiest to extract from.

## Hugging Face Papers (what's trending / curated daily)

HF curates a daily set of notable arXiv papers with community discussion — useful for "what's hot right now".
- Use the Hugging Face connector if available (search papers/models/datasets).
- Otherwise `web_fetch`:
  - `https://huggingface.co/papers` (today's trending)
  - `https://huggingface.co/papers?date=YYYY-MM-DD` (a specific day)
  - `https://huggingface.co/papers?q=KEYWORD` (search)
- HF paper pages link back to the arXiv id and surface upvotes/discussion — a rough popularity signal, not a quality signal. Treat it as triage, not endorsement.

## bioRxiv / medRxiv (biomechanics, sports science, biology-adjacent)

Use the bioRxiv connector. Relevant tools: `search_preprints`, `search_published_preprints` (find ones that reached a journal), `get_preprint` (full metadata by DOI), `get_categories`.
- Relevant categories: bioengineering, biophysics, neuroscience, physiology, scientific-communication-and-education (for methods/biomechanics, filter by keyword too).
- For sports-sci biomechanics, search terms like "gait", "kinematics", "ACL", "musculoskeletal", "OpenSim", "markerless".
- bioRxiv preprints often lack rigorous peer review — weight the methodology critique accordingly and check `search_published_preprints` for a vetted version.

## Cross-checking and recency verification

- Confirm a preprint's status: search the title to see if a peer-reviewed version exists (journal, conference). Prefer linking the published version while noting the preprint date.
- For impact/lineage, a `web_search` of the title plus "cited by" or a Semantic Scholar / Google Scholar lookup gives rough citation counts and the "references" needed for the "read next" section. Citation count is a lagging signal — a 2-week-old preprint with zero citations can still be the most important thing in the field.
- Always report the actual date. If you can't establish recency, say so rather than implying freshness.

## When a source is unavailable

If a needed connector isn't enabled, fall back to `web_search` + `web_fetch` against the source's website and tell the user which source you couldn't query directly, so they can enable the connector for better results.
