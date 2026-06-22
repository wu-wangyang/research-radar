# Analysis Rubric

The difference between a useful note and a useless one is judgment. Apply all four layers to every paper. Each has a "look for" list and a quality bar. A worked good-vs-bad example is at the bottom.

First, extract the skeleton (so the analysis has something to bite on):
- **Problem**: what gap or failure of prior methods does it target?
- **Contribution**: the one or two things the authors claim are new.
- **Method**: the approach in plain language — architecture, training signal, key trick.
- **Evidence**: datasets, baselines compared against, metrics, ablations, hardware (for robotics: sim only or real-robot?).

Then the four layers:

## 1. Methodology critique

Look for:
- **Baselines**: are the comparisons fair and current, or against weak/old methods? Missing an obvious competitor?
- **Evaluation breadth**: one environment/dataset or many? Does the claim generalize beyond what was tested?
- **Statistics**: seeds, error bars, significance — or a single run? For sports-sci/biomech: sample size, subject diversity, was it cross-validated?
- **Ablations**: do they isolate what actually drives the gains, or is it a bundle?
- **Reproducibility**: code released? checkpoints? enough detail to reimplement?
- **Real vs sim** (robotics): does it transfer to hardware, or is it sim-only with a sim-to-real promissory note?

Bar: at least one *specific, substantiated* critique. Not "evaluation could be stronger" but "only evaluated on flat-ground locomotion, so the rough-terrain claim is unsupported."

## 2. Novelty vs prior work

Look for:
- What lineage does this extend? Name predecessors (e.g. for humanoid RL: DeepMimic → AMP → later imitation/whole-body work).
- Is the contribution a genuinely new mechanism, or a known idea applied to a new domain, or an engineering/scale result? All can be valuable — label which.
- Does it actually beat the thing it claims to beat, or just match it with caveats?

Bar: name at least one predecessor and state plainly where this sits — "new mechanism", "known method, new domain", "scale/engineering result", or "incremental".

## 3. Relevance to the user's work

The user works across: markerless motion capture, ML-based injury prediction, humanoid/legged robot control, differentiable biomechanics, and clinical data-collection systems. Be concrete:
- *How* would they use this — a method to try, a baseline to beat, a dataset to use, a competitor to watch?
- Or say plainly: "Not relevant to your current threads because it's about X, which doesn't touch mocap/injury/control."

Bar: an actionable "so what for you", or an explicit no. Never vague.

## 4. What to read next

Look for:
- The 1–2 references this paper rests on that the user should read first if the topic is new to them.
- Any follow-on or competing work worth tracking.
- Link these as `[[wikilinks]]` so they become stubs in the vault.
- **One concrete action**, not just reading: clone-and-run the repo, try the method on the user's own data, reproduce the headline number, or contact the author. Make it small and specific.
- **What would change the verdict**: 1–2 questions whose answers would flip your assessment (e.g. "does it hold on rough terrain?", "is the gain still there with a matched baseline?"). These double as active-recall prompts in the vault.

Bar: name specific papers/works (not "the related work section"), and give one action plus at least one verdict-changing question.

## Deep-tier tools (apply only on the Deep depth tier)

These are slow and adversarial — reserve them for the 1–2 papers that actually matter. They're what turn a competent note into a sharp one.

### Inversion / pre-mortem

Instead of asking "is this right?", assume the headline result is fragile and ask **"how would I make it fail?"**:
- If you had to get the opposite result, what would you change — dataset, seed, baseline, hyperparameters, environment?
- Which single design choice is the result most sensitive to, and did they test that?
- Pre-mortem: it's a year later and this didn't replicate. What's the most likely reason? Is that reason ruled out by the paper, or just unaddressed?

Output: the most probable failure mode, and whether the paper closes it. This usually surfaces the real weakness faster than a strengths/weaknesses list.

### First-principles strip

Strip the framing, the branding, and the related-work positioning. Ask **"what is the actual new thing here, reduced to its core?"**:
- State the contribution in one plain sentence with no adjectives and no method name.
- Which parts are genuinely new mechanism, and which are standard components doing standard jobs?
- If the new mechanism were removed, how much of the reported gain would survive (per their ablations)? If they don't ablate it, say so — that's a gap.

Output: a one-line "what's really new" statement that you can defend, which sharpens the novelty layer and catches scale/engineering results dressed up as conceptual breakthroughs.

## Worked example (good vs bad)

Suppose the paper is a new whole-body humanoid controller trained with RL in sim, evaluated on a single robot doing locomotion.

**Bad TL;DR (reject):** "This paper presents a reinforcement learning approach for humanoid robot control achieving strong performance." — restates the abstract, no verdict, no judgment.

**Good TL;DR (accept):** "Clean whole-body RL controller with a real-robot demo, but every result is single-robot, single-task locomotion — the 'general control' framing outruns the evidence. Worth watching the method, not citing the generality claim."

**Good critique sentence:** "No comparison against [predecessor] under the same reward, so the reported gain could be tuning rather than the new architecture."

**Good relevance sentence:** "Directly useful as a baseline for your legged-control work; the reward formulation is reusable, but you'd need to add the perception stack they assume away."

That's the level. Opinionated, specific, defensible.
