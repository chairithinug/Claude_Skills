# Claude_Skills

A workspace for authoring [Claude AI Skills](https://platform.claude.com/docs/en/agents-and-tools/agent-skills) — small, triggered playbooks that get loaded into Claude's context when a relevant task comes up.

This repo holds the source folders, distributable `.skill` archives, the authoring standard, and HTML demos for each skill.

## Repository layout

```
Claude_Skills/
├── README.md            # this file
├── CLAUDE.md            # always-loaded session pointer + non-negotiables
├── STANDARDS.md         # encyclopedic authoring playbook
├── _template/           # scaffolding for new skills (SKILL.md + evals.md)
├── <skill-name>/        # one folder per skill
│   ├── SKILL.md
│   └── references/      # optional, one level deep only
├── <skill-name>.skill   # distributable archive (zip of the folder)
└── <skill-name>.html    # optional public-safe HTML demo
```

## Skills in this repo

| Skill | Trigger | What it does |
|---|---|---|
| [`ai-fluency-planning/`](ai-fluency-planning/) | `/ai-fluency-planning` | Conducts a focused pre-execution interview using the AI Fluency 4D Framework (Delegation, Description, Discernment, Diligence) and produces a markdown AI Project Brief the user can reference throughout the project. |
| [`deciding/`](deciding/) | `/deciding` | Walks a real decision through options, criteria, trade-offs, key unknown, reversibility, pre-mortem. Recommends only when the criteria clearly favor one option. |
| [`devil-advocating/`](devil-advocating/) | `/devil-advocating` | Builds the strongest case against the user's position. No balance, no recovery path. |
| [`executive-lensing/`](executive-lensing/) | `/executive-lensing` | Stress-tests a problem through CEO, CFO, COO, CMO, CTO, CHRO lenses, surfacing the distinct concern each function would raise. |
| [`explaining/`](explaining/) | `/explaining` | Gives the answer with full reasoning visible, then closes with a pattern-recognition cue for the next similar problem. |
| [`fortune-telling/`](fortune-telling/) | `/fortune-telling` | Multi-tradition divination (Thai day-of-week, Chinese BaZi, Vedic, Western, Japanese Rokuyō). Picks one primary tradition + at most one cross-check; gives a verdict, not a lecture. For entertainment. |
| [`negotiating/`](negotiating/) | `/negotiating` | Structured negotiation prep — interests, BATNA, cognitive traps, opening and concession architecture, pre-mortem. Also auto-fires on real upcoming negotiations (salary, vendor, partnership, fundraise). |
| [`quick-answering/`](quick-answering/) | `/quick-answering` | Fast minimal answer. No frameworks, no scaffolding, no caveats unless load-bearing. |
| [`researching-topics/`](researching-topics/) | `/researching-topics` | Conducts substantive topic research via a six-step methodology (frame → map → plan sources → execute → synthesize → verify). Three modes (quick-scan, deep-dive, compare-options); layered output with TL;DR, confidence-labeled findings, steel-manned competing views, open questions, and sources. |
| [`thai-dish-picking/`](thai-dish-picking/) | `/thai-dish-picking` | Suggests 3 varied Thai dishes when the user can't decide what to eat. Spans regions and categories deliberately, avoids the famous-20 autopilot, searches bilingually for less-obvious dishes. |
| [`token-optimizing/`](token-optimizing/) | `/token-optimizing` | Compresses prompts, RAG context, few-shot blocks, and agent loops without losing load-bearing content. Triages cache → batch → route → bound → compress → rewrite before touching the prompt. Ships with worked example, trigger eval (20 cases), and quality eval (8 cases). |
| [`working-through/`](working-through/) | `/working-through` | Coaches the user to the answer instead of giving it — provides the framework, asks them to apply it, reacts to their attempt. |

## SWOT — per skill

A short read on what each skill is good at, where it falls down, where it could grow, and what could break it. Strictly about the skill's mechanics — not about who's using it.

### `ai-fluency-planning`
- **Strength** — produces a reusable artifact (the brief) that gets referenced throughout the project, not a one-shot plan; applies a published framework rather than ad-hoc structure.
- **Weakness** — the full interview can feel heavy on simple projects; relies on the user articulating Discernment criteria, which many people find hard upfront.
- **Opportunity** — could ship template variants for common project types (memo, code project, research synthesis); could integrate with `/deciding` for project-go/no-go gating.
- **Threat** — risk of becoming a procrastination tool — endless planning without execution. Output should commit the user to a concrete start.

### `deciding`
- **Strength** — six-step structure surfaces reversibility and the key unknown explicitly, not just options/criteria; only recommends when criteria clearly favor one option.
- **Weakness** — output quality depends entirely on whether the user articulates their criteria honestly; structured output can mask shaky inputs.
- **Opportunity** — pairs naturally with `/devil-advocating` for stress-testing the recommended option; could add domain references (hire/fire, vendor selection, acquisition).
- **Threat** — pseudo-rigor risk — the framework can make a flimsy decision look thorough without surfacing the actual hard trade-off.

### `devil-advocating`
- **Strength** — forces a steel-manned argument against the user's position; no balance, no recovery path, no hedging — the brief is the point.
- **Weakness** — output is intentionally one-sided; misuse as the only input would be epistemically distorting.
- **Opportunity** — best chained after `/deciding` for full stress-test cycle; could add a counter-stance parameter for unusual oppositions.
- **Threat** — emotionally taxing on value-laden personal decisions; user must be in stress-test mode, not validation mode.

### `executive-lensing`
- **Strength** — surfaces concerns from up to six functional perspectives, skipping irrelevant ones; passive trigger logic catches strategic decisions where the skill wasn't invoked explicitly.
- **Weakness** — lens depth depends on assumptions about each role; can collapse into vague abstractions if the user's input is thin.
- **Opportunity** — could extend with industry-specific lenses (regulatory, security, founder-investor); could pair with `/deciding` for a full strategic pass.
- **Threat** — risk of generic role-play if context lacks specifics — the lenses sound impressive while saying nothing testable.

### `explaining`
- **Strength** — pattern-recognition cue at the end makes each explanation transferable to the next similar problem, not one-off.
- **Weakness** — quality of the cue depends on Claude's domain depth; thin domains produce thin cues.
- **Opportunity** — could include a reference file of common patterns (logical fallacies, distributed-systems trade-offs, statistical traps) to scaffold richer cues.
- **Threat** — conflicts with `/working-through`; if both are invoked, the user is asked to pick — that friction may annoy.

### `fortune-telling`
- **Strength** — multi-tradition coverage with explicit "skip what can't be verified" honesty; for-entertainment framing is built in once-per-session, not repeated.
- **Weakness** — technical accuracy on Rokuyō and BaZi day-stems requires ephemeris/calendar lookups Claude lacks; readings rely on traditions that don't need precise computation.
- **Opportunity** — could integrate calendar/ephemeris APIs for accurate lunar and astronomical data; could add per-tradition reference files for depth.
- **Threat** — readers may act on predictions for high-stakes decisions despite the disclaimer; medical/legal/financial guardrails must stay firm.

### `negotiating`
- **Strength** — explicit positive and negative trigger cases (this is the strongest description in the repo for accurate firing); ethics check is built into the workflow rather than tacked on.
- **Weakness** — body is the longest of the reasoning skills; full 8-step prep is overkill for tactical mid-negotiation moments.
- **Opportunity** — could split into prep-mode and tactical-mode reference files; could add domain references (salary, vendor, fundraise) with specific anchoring guidance.
- **Threat** — analysis paralysis when timing is the actual bottleneck; skill should detect "this is moving fast" and switch to tactical mode automatically.

### `quick-answering`
- **Strength** — uncompromising brevity rule — no scaffolding, no caveats unless load-bearing; forces past default verbosity.
- **Weakness** — loses to mode conflicts when other skills want to add structure; can hide nuance on genuinely complex questions.
- **Opportunity** — strong companion to verbose skills — chained as a "now compress that" follow-up after a long output.
- **Threat** — misapplication on ambiguous questions risks confidently-wrong short answers; skill must flag ambiguity rather than guess.

### `researching-topics`
- **Strength** — forced six-step methodology with three modes; layered output explicitly separates fact from inference and labels each finding with a confidence level; steel-mans competing views rather than balancing them.
- **Weakness** — methodology overhead is wasted on simple lookups; user has to recognize when their question warrants the full treatment vs. a direct answer (the description's negative-trigger list helps but isn't perfect).
- **Opportunity** — could ship reference files for domain-specific source plans (financial, technical, regulatory, scientific); could chain with `/deciding` when the research feeds a decision; could add per-mode trigger evals.
- **Threat** — confidence labels are only as honest as Claude's calibration; over-confident "high confidence" labels on weakly-sourced findings would defeat the skill's main value proposition.

### `thai-dish-picking`
- **Strength** — bilingual search guidance (Thai + English) and explicit autopilot-avoidance rules; three worked examples baked in for diversity, full agency, and constrained modes.
- **Weakness** — Bangkok-availability weighting may be off for users elsewhere in Thailand or for diaspora contexts.
- **Opportunity** — could add dietary-restriction reference files (vegetarian, halal, gluten-free); could integrate with location-aware data for real-time availability.
- **Threat** — quality depends on freshness of Thai-language search results; without web search, the skill falls back to memory which over-represents the famous twenty.

### `token-optimizing`
- **Strength** — triages cache → batch → route → bound → compress → rewrite before touching the prompt; ships with both trigger eval (20 cases) and quality eval (8 cases) plus a worked example.
- **Weakness** — tokenizer estimates are approximations; non-English content needs the real tokenizer to count accurately.
- **Opportunity** — could ship reference scripts for token counting across providers; could add a per-provider pricing reference that updates as provider docs change.
- **Threat** — aggressive compression on safety-relevant content risks cutting material the original safety review depended on; skill must refuse cuts in those zones.

### `working-through`
- **Strength** — coaches the user to derive the answer rather than handing it over; matches learning-by-doing pedagogy.
- **Weakness** — requires user willingness to engage; not appropriate for time-pressed work or when the user simply needs the answer.
- **Opportunity** — could integrate domain-specific reasoning frameworks (debugging, math, design critique) as reference files, each scaffolding a different reasoning shape.
- **Threat** — can feel patronizing if the user wanted `/explaining` instead; skill should detect frustration signals and offer to switch.

## Authoring a new skill

The full process is in [STANDARDS.md](./STANDARDS.md). The short version:

1. Copy `_template/` to a new gerund-named folder (e.g., `summarizing-papers/`).
2. Write **`evals.md` first** — three scenarios that test the gap the skill should close. Establish baseline performance without the skill.
3. Draft `SKILL.md` to address the eval failures only. No anticipatory content.
4. Iterate on the description first (discovery), then the body (output quality).
5. Build the `.skill` archive: `zip -r <name>.skill <name>/ -x "*.DS_Store"`.

## Conventions worth flagging

- **Folder name = frontmatter `name` field = slash-command trigger = gerund form.** A skill named `deciding` is invoked with `/deciding` — one canonical string per skill.
- **`SKILL.md` body ≤ 500 lines.** Past that, split into `references/<topic>.md`, one level deep. Never nest references.
- **No secrets, anywhere.** No API keys, no `process.env`, no `.env` files, no PII — in skill files or HTML demos. This repo is public.
- **HTML demos must satisfy the public-GitHub safety contract** in [STANDARDS.md §12](./STANDARDS.md#12-html-demo-artifact--public-github-safety-contract). Single-file, runs from `file://`, no API calls to provider endpoints, no key inputs without explicit warnings.
- **Anthropic's [authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices) supersede everything here** when they conflict.

## Installing skills from this repo

Each `.skill` file is a zip of its source folder. The exact install path depends on your Claude / Cowork setup — common flows are dropping the folder into a local skills directory, importing the `.skill` archive through the Cowork plugin UI, or syncing the folder into a plugin source repo and reinstalling the plugin.

## License

Personal authoring workspace. Skills here encode personal reasoning preferences and may not generalize. Borrow what's useful.
