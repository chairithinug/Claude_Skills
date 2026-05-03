# Skill Authoring Standards

The authoritative playbook for skills in this repository. Anything that conflicts with [Anthropic's Skill authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices) defers to Anthropic — they ship the runtime, they win.

This document is the reference. The always-loaded pointer is [CLAUDE.md](./CLAUDE.md). New skills start from [_template/](./_template/).

---

## 1. What a skill is and isn't

A skill is a `SKILL.md` file with YAML frontmatter, optionally accompanied by `references/`, `scripts/`, and `assets/`. Claude pre-loads only the frontmatter (`name` + `description`) at session start. The body of `SKILL.md` is read only when the description triggers; reference files are read only when the body points to them. This is **progressive disclosure** and it is the entire reason the system scales to dozens of skills without flooding context.

Skills are **not** general system prompts. Do not write a skill to add personality, voice, or always-on behavior — those belong in `CLAUDE.md` or project instructions. A skill encodes a *triggered playbook* for a specific class of task.

---

## 2. Folder structure

Each skill lives in its own folder named exactly the same as the frontmatter `name` field.

```
<skill-name>/
├── SKILL.md            # required — the entry point
├── references/         # optional — long-form, loaded on demand
│   ├── <topic-a>.md
│   └── <topic-b>.md
├── scripts/            # optional — executable helpers
│   └── <tool>.py
└── assets/             # optional — templates, fonts, fixtures
```

Rules that bite:

- **One level deep.** Reference files may be linked from `SKILL.md` only. A reference linking to another reference produces partial reads — Claude will `head -100` it and miss content. If you find yourself wanting to nest, hoist all entry points up to `SKILL.md`.
- **No `index.md` in references.** Just topic-named files. Discovery happens through the body of `SKILL.md`, not through a sub-table-of-contents.
- **`assets/` is for static input**, not output. Output goes wherever the skill writes it (your outputs folder, the user's workspace, etc.).

---

## 3. Frontmatter rules (Anthropic-mandated)

```yaml
---
name: my-skill-name
description: >
  Third-person sentence describing what the skill does and when to use it.
  Include specific trigger phrases. Max 1024 chars.
---
```

Hard requirements:

- `name`: max 64 chars, lowercase letters / numbers / hyphens only. **Cannot** contain `anthropic` or `claude`. No XML tags. The folder name must match.
- `description`: non-empty, max 1024 chars, no XML tags. Must include both **what the skill does** and **when to use it**.

Style requirements (enforced by review, not by the runtime):

- Third person. Write "Analyzes…" not "I analyze…" or "You can use this to…". The description is injected into the system prompt; first/second person breaks Claude's discovery.
- Specific. "Helps with documents" is unusable; "Extracts text and tables from PDFs, fills forms, merges documents" is.
- Trigger-explicit. If the skill has an invocation phrase (slash command, keyword), name it inside the description verbatim — that is what discovery matches against.

---

## 4. Naming convention

**Default: gerund form.** `processing-pdfs`, `analyzing-spreadsheets`, `working-through`, `executive-lensing`. Gerunds describe activities, which is what skills are.

**Acceptable alternatives** when gerunds are awkward: noun phrases (`pdf-processing`, `spreadsheet-analysis`) or imperatives (`process-pdfs`). Pick one pattern per family and stick to it.

**Avoid:** vague names (`helper`, `utils`, `tools`), generic categories (`documents`, `data`, `files`), and reserved words (`anthropic-*`, `claude-*`).

**Slash-command triggers match the folder/name.** A skill named `deciding` is invoked with `/deciding`. The slash command is the gerund-form name with a `/` prefix — one canonical string per skill, used as both folder name and invocation. The trigger goes inside the description as `Use when the user types /<name>`. This is intentional: the earlier short-trigger / long-name split (e.g., trigger `/decide` vs name `deciding`) was abandoned because it created two strings for one identity, which confused both authors and users.

---

## 5. Writing the description

The description is the **single most important field in your skill**. Claude scans descriptions to decide which skills to read. A bad description means a perfect skill body never gets loaded.

Required ingredients:

1. **What** — what the skill does, in concrete verbs. Not "helps with X" — "extracts X from Y," "generates X using Y."
2. **When** — the contexts and trigger phrases that should fire it. Be explicit: "Use when the user types /deciding" or "Use whenever the user mentions PDFs, forms, or document extraction."
3. **Specificity** — name the artifacts (`.xlsx`, `commit messages`, `PDFs`), not categories (`files`, `things`).

Length guidance: 1–3 sentences. Skills that need more disambiguation can use up to ~1024 chars but most fit in 200–400.

**Good:**
> Extracts text and tables from PDF files, fills forms, merges documents. Use when working with PDF files or when the user mentions PDFs, forms, or document extraction.

**Bad:**
> Helps you handle PDF stuff. (Vague verbs, vague trigger, first-person framing.)

A note on tone: older notes in this repo suggested making descriptions "slightly aggressive" because Claude undertriggers. Anthropic's guidance is just to be **specific** — well-written specifics solve the under-triggering problem without forcing tone. Stay specific; do not write descriptions that sound desperate.

---

## 6. SKILL.md body conventions

The body is read only when the skill triggers. Treat every token as costing once it loads. Default assumption: Claude is already smart — only add what Claude does not already know.

**Canonical four-section structure** for skills in this repo:

```markdown
# <Title> — <Tagline>

<Lead paragraph — what this skill does and the philosophy behind it.>

## When to use this

- <Trigger condition 1>
- <Trigger condition 2>

## Steps / Workflow

<Numbered steps. For complex skills, include a copy-paste checklist.>

## Output format

- <Format rule 1>
- <Format rule 2>
- <No sycophantic opener / no trailing summary>

## Edge cases

**<Case A>**: <Handling.>

**<Case B>**: <Handling.>
```

Add a fifth section only when warranted:

- **Examples** — when output quality depends on seeing input/output pairs (e.g., commit message style).
- **Reference pointers** — for skills with `references/`, list the topics with one-line "load when…" descriptions.
- **Anti-patterns** — distinct from edge cases. Edge cases handle unusual inputs *while* running the skill; anti-patterns name behaviors the skill should refuse or flag (e.g., compressing safety-critical content, fabricating data the skill can't verify). Use when there's a clear set of "don't do this even if asked" items worth listing separately.

### Long-skill variant — top-level `## Step N — Title` headings

The `## Steps / Workflow` wrapper above is the default for skills where the workflow fits naturally as a numbered list of short steps. For skills with substantial multi-step workflows — typically 5+ distinct steps where each step needs its own paragraphs, tables, sub-bullets, or code — the long-skill variant uses top-level h2 headings per step instead of a wrapper:

```markdown
# <Title> — <Tagline>

<Lead paragraph.>

## When to use this
- <…>

## Step 0 — <Title of preflight or triage step>
<Substantial content for this step.>

## Step 1 — <Title of next step>
<Substantial content.>

## Step 2 — <…>
<…>

## Output format
<…>

## Edge cases
<…>
```

Both patterns are canonical; pick by the shape of the workflow, not by preference. The rest of the canonical structure (When to use this, Output format, Edge cases, optional Examples / Reference files / Anti-patterns) applies in both variants.

When in doubt, default to the wrapper. Skills that grew into the long variant: `token-optimizing`, `researching-topics`, `ai-fluency-planning` — all over 200 lines with formal multi-step methodology where each step has its own sub-structure.

Length cap: **500 lines for `SKILL.md`**. If you cross it, split into reference files (see §7).

---

## 7. Progressive disclosure

The structure should match how Claude actually loads files:

1. **Frontmatter** — pre-loaded for every session. Optimize for discovery.
2. **`SKILL.md` body** — loaded when the skill triggers. Optimize for the common path.
3. **Reference files** — loaded on demand. Optimize for completeness; depth is fine here.

Decision tree:

- Body content under 500 lines and one cohesive workflow → keep it all in `SKILL.md`.
- Body crosses 500 lines, or covers multiple sub-domains → split into `references/<topic>.md` files; `SKILL.md` becomes a router.
- Reference file exceeds 100 lines → add a table of contents at the top so partial reads still see the scope.
- Multiple sub-domains with no shared workflow (e.g., AWS vs GCP vs Azure) → one reference file per domain, with `SKILL.md` listing "load X when Y."

Example router-style `SKILL.md` body:

```markdown
## Available domains

**Finance** — revenue, ARR, billing → see [references/finance.md](references/finance.md)
**Sales** — pipeline, accounts → see [references/sales.md](references/sales.md)
**Product** — feature usage → see [references/product.md](references/product.md)
```

Do not nest references. A reference linking another reference will be partially read.

---

## 8. Patterns library

Reach for these when they fit. Do not force any of them.

### Workflow checklist
For multi-step tasks, give Claude a copy-paste checklist that gets reproduced in the response.
```markdown
## Steps

Copy this checklist and tick items off as you go:

- [ ] Step 1: <…>
- [ ] Step 2: <…>
- [ ] Step 3: <…>
```

### Feedback loop
When validation is cheap and failure is costly:
```markdown
1. Make the change.
2. Run `python scripts/validate.py`.
3. If validation fails, fix and rerun. Do not proceed until it passes.
4. Continue.
```

### Template (strict vs flexible)
Strict templates use `ALWAYS use this exact structure`. Flexible templates say `here is a sensible default — adapt as needed`. Pick deliberately.

### Examples
When style is hard to describe but easy to recognize:
```markdown
**Example 1:**
Input: <…>
Output: <…>

**Example 2:**
Input: <…>
Output: <…>
```

### Conditional routing
For multi-path skills:
```markdown
1. Determine the type:
   - **Creating new content?** → Follow §A.
   - **Editing existing content?** → Follow §B.
2. <Continue per branch.>
```

---

## 9. Content rules

- **Concise is mandatory.** Cut every sentence that explains a thing Claude already knows. Never define what a PDF is. Never explain that libraries exist.
- **Match degrees of freedom to fragility.** High freedom (text guidance) for tasks with multiple valid approaches. Low freedom (exact commands, no flags) for tasks where consistency is critical or operations are destructive. Medium (parameterized scripts, templates) in between.
- **Consistent terminology.** Pick one term per concept and stay with it. Don't mix "field / box / element / control"; pick one.
- **No time-sensitive language.** Don't write "as of late 2025…" Use an "Old patterns" section for anything deprecated, in a `<details>` foldout.
- **No first/second person.** Frontmatter and body alike — write in third person or imperative.

---

## 10. Authoring loop (eval-first)

Skills written in a vacuum drift. The order is:

1. **Identify the gap.** Run a representative task in Claude *without* the skill. Document what's missing — wrong format, missing context, hallucinated imports, whatever.
2. **Build 3 evals before writing the skill.** Each eval = `{ query, expected_behavior[], optional input files }`. Save them in `evals.md` next to `SKILL.md` (or a `evals/` subfolder if multiple eval artifacts exist).
3. **Establish baseline.** Run the evals without the skill. Note failures.
4. **Write minimal SKILL.md.** Just enough to address the eval failures. No anticipatory content.
5. **Run evals with the skill.** Compare to baseline.
6. **Iterate on description first.** If discovery fails (skill doesn't trigger), the description is wrong. Tune it before tuning the body.
7. **Iterate on body.** If discovery works but output is wrong, tune steps/output format/edge cases.
8. **Test across models** if the skill will run on more than one. Haiku may need more guidance than Opus.
9. **Package** as a `.skill` file when stable.

### Subjective-skills exemption

Quality evals are **mandatory for skills with objectively verifiable outputs** — file transformations, data extraction, code generation, fixed-format reports, anything where success can be checked against a rubric. The token-optimizing skill is the canonical example: token count goes down, load-bearing content survives, both are measurable.

Quality evals are **optional for subjective skills** — reasoning, coaching, persuasion, judgment-laden analysis, anything where the "right" output is a matter of taste, framing, or context. Forcing quality grading on a skill like `/devil-advocating` produces noise (graders disagree) and tempts overfitting (the skill optimizes for whatever graders happen to score well, which is not the same as "argues well"). For these skills, the human review step in the iteration loop carries the load.

**Trigger evals are recommended for every skill regardless of category.** A skill that doesn't trigger reliably is broken even if its body is brilliant. 10–20 trigger queries (mix of should-fire and should-not-fire) plus `run_loop.py` is the cheapest path to confidence here.

**Trigger eval file format.** `<skill>/evals/trigger-eval.json` must be a **flat top-level JSON array** of objects, each with `query` (string), `should_trigger` (bool), and optionally `category` (string for grouping in reports). No wrapper object, no `_comment` key — `run_loop.py` calls `json.load` and iterates the result directly, so a wrapper breaks the loop with a `TypeError`. Conventional shape:

```json
[
  {"query": "explicit slash command or sentence", "should_trigger": true, "category": "explicit_invocation"},
  {"query": "near-miss that should not fire", "should_trigger": false, "category": "adjacent_skill_territory"}
]
```

Aim for ~10 should-fire and ~10 should-not-fire. Negatives carry the load — pick *near-misses* (adjacent skills, theoretical questions, factual lookups in the same domain) rather than obvious noise. See skill-creator's `references/schemas.md` for the canonical reference.

`_template/evals.md` provides the scaffold for step 2.

### Persisting loop results

When you run skill-creator's `run_loop.py` against a skill's trigger eval, save a lightweight summary to `<skill>/evals/loop-results.md`. The summary captures:

- Date and model used
- Baseline vs. iterated train/test scores
- The best description suggested by the loop
- Your decision (accepted / rejected / modified) and a one-line reason
- Any patterns worth noting (which negatives consistently fired, which positives consistently missed)

`_template/loop-results.md` is the scaffold.

Raw run-loop output (HTML reports, full JSON dumps, candidate-description history) lives in `<skill>/evals/loops/<date>/` and is **gitignored** — large, reproducible from the eval set, and not worth bloating the repo. The committed summary file is what future-you will actually read.

Re-run the loop when:
- The description has been substantively changed
- A major model update lands (loop scores can drift on the same description as Claude evolves)
- The eval set is expanded or rebalanced

---

## 11. Post-creation handoff (this repo's convention)

When a skill is finished and tested locally, the author hands it back to the user with this exact message:

> "<skill-name> is ready. To activate it, please install the skill (drop the folder into your skills directory or run your install flow). Once it's installed, send me the magic line and I'll build a runnable demo:
>
> > Hey Claude—I just added the "<skill-name>" skill. Can you make something amazing with it?"

Why a magic line: it doubles as a discovery test. If Claude doesn't recognize the skill name from the description after installation, the description is broken and the skill won't fire on real use either.

When the user sends the magic line, build a single-file HTML artifact that demonstrates the skill. See §12 for the safety contract.

---

## 12. HTML demo artifact — public-GitHub safety contract

Demos in this repo end up on public GitHub. Every demo must satisfy all of these:

**Forbidden in source:**
- Any string matching `sk-ant-`, `ANTHROPIC_API_KEY`, `Bearer sk-`, or any OpenAI/Anthropic/third-party key shape.
- `process.env.*` references that imply a key is expected at runtime.
- `os.environ` reads, `.env` files, dotenv loaders.
- Hardcoded internal URLs, internal bearer tokens, OAuth client secrets.
- Personal email, address, phone, or other PII of the author or user.
- Direct calls to `https://api.anthropic.com/*` or any provider API endpoint.
- Comments suggesting where to paste a key (e.g., `// add your key here`).

**Required:**
- **Single HTML file.** CSS and JS inline. No external JS files in the same folder (avoids accidental key files sitting next to the HTML).
- **Runs from `file://` and from GitHub Pages.** No build step, no server, no local proxy.
- **Dependencies via well-known CDNs only** (Tailwind Play CDN, Chart.js via cdnjs, Mermaid via jsDelivr). Pin a version.
- **No tracking.** No analytics scripts, no `fetch()` to author-controlled domains.
- **Pure client-side compute** by default. The demo should illustrate the skill's framework, output format, or flow — not call an LLM.
- **If LLM calls are genuinely needed**, accept a user-pasted key via an input field, store in `localStorage` only after the user submits, and warn in the UI: *"Your key is stored locally in this browser. Do not commit demos containing pasted keys."* Even then, prefer not to do this — public GitHub viewers should not be tempted to paste keys into a random page.

**Pre-publish checklist** (run mentally or via grep before delivering):

```
- [ ] grep -E "sk-(ant|live)|ANTHROPIC_API_KEY|process\.env|os\.environ|Bearer "
- [ ] grep "api.anthropic.com"
- [ ] No .env, no config files alongside the HTML
- [ ] All <script src="..."> URLs are public CDNs
- [ ] No author PII in comments or visible text
- [ ] Opens cleanly when double-clicked from disk
```

If a demo cannot be made safe under these rules, write a Markdown explainer instead and tell the user why an HTML demo isn't appropriate for that skill.

---

## 13. Packaging (`.skill` files)

A `.skill` file is the distributable archive. Conventions:

- Filename matches the skill name: `<skill-name>.skill`.
- Lives at the repo root, alongside the skill folder.
- Regenerate after any rename or substantive content change. A stale `.skill` ships old metadata to whoever installs it.
- The folder is the source of truth; the `.skill` is a build artifact.

This repo currently has `.skill` files from the pre-rename era — they reference old names and should be regenerated next time a skill is reinstalled.

---

## 14. Quick checklist for a new skill

```
- [ ] Identified a real, repeated gap (not anticipated)
- [ ] Wrote 3 evals in evals.md
- [ ] Established baseline performance without the skill
- [ ] Folder name = frontmatter name = gerund or accepted alt
- [ ] Description: third-person, what + when, ≤1024 chars, includes trigger token
- [ ] Body ≤500 lines; references split if longer
- [ ] All references one level deep from SKILL.md
- [ ] No time-sensitive content; consistent terminology
- [ ] Output format section explicitly bans sycophantic openers / trailing summaries (default for this repo)
- [ ] Tested across all target models
- [ ] Post-creation handoff message sent
- [ ] HTML demo passes §12 safety contract
- [ ] .skill packaged after rename or content change
```

---

## 15. Divergences from earlier internal notes

For traceability — earlier notes in this project suggested patterns that this standard now overrides. Anthropic's doc takes precedence in all cases.

| Earlier note | This standard |
|---|---|
| "Make descriptions slightly aggressive — Claude undertriggers." | Be specific. Specificity solves under-triggering without forced tone. |
| Skill name = slash-command trigger (`decide`, `csuite`). | Skill name = folder = trigger token, all gerund (`/deciding`, `/executive-lensing`). The earlier short-trigger / long-name split was abandoned; one canonical string per skill. |
| Optional iteration loop. | Eval-first is mandatory. Three evals before a body is written. |
| `.skill` packaging is the install artifact. | Folder is the source of truth. `.skill` is a regenerated build artifact. |

---

*End of standard. When this document and Anthropic's docs disagree, Anthropic wins. Update §3, §4, §5, §7 here when Anthropic updates upstream.*
