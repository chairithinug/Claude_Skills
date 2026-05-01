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
| [`thai-dish-picking/`](thai-dish-picking/) | `/thai-dish-picking` | Suggests 3 varied Thai dishes when the user can't decide what to eat. Spans regions and categories deliberately, avoids the famous-20 autopilot, searches bilingually for less-obvious dishes. |
| [`token-optimizing/`](token-optimizing/) | `/token-optimizing` | Compresses prompts, RAG context, few-shot blocks, and agent loops without losing load-bearing content. Triages cache → batch → route → bound → compress → rewrite before touching the prompt. Ships with worked example, trigger eval (20 cases), and quality eval (8 cases). |
| [`working-through/`](working-through/) | `/working-through` | Coaches the user to the answer instead of giving it — provides the framework, asks them to apply it, reacts to their attempt. |

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
