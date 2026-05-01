# Working in this folder

This is Mew's skill-authoring workspace. Every session in this folder is about building, editing, evaluating, or demoing Claude AI Skills. The full playbook is in [STANDARDS.md](./STANDARDS.md) — read it before creating or editing any skill. Scaffolding starts at [_template/](./_template/).

## Non-negotiable rules

1. **No secrets, anywhere.** No `ANTHROPIC_API_KEY`, no `sk-ant-…`, no `process.env.*` references, no `.env` files, no internal URLs, no PII. This applies to skill files *and* HTML demos. Demos in this repo end up on public GitHub.
2. **Folder name = frontmatter `name` field = slash-command trigger = gerund.** A skill named `deciding` is invoked with `/deciding`; one canonical string per skill. The trigger lives in the description as `Use when the user types /<name>`.
3. **Eval-first.** Three eval scenarios in `evals.md` before the body of a new `SKILL.md` gets written. Anticipatory documentation is the failure mode this rule prevents.
4. **`SKILL.md` body ≤ 500 lines.** Past that, split into `references/<topic>.md`, one level deep from `SKILL.md`. Never nest.
5. **Anthropic doc wins.** When STANDARDS.md and [Anthropic's best-practices page](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices) disagree, defer to Anthropic. Update STANDARDS.md to match.

## Post-creation handoff (the magic line)

After writing a new skill, end with this exact message to the user:

> *<skill-name>* is ready. To activate it, please install the skill (drop the folder into your skills directory or run your install flow). Once it's installed, send me:
>
> > Hey Claude—I just added the "<skill-name>" skill. Can you make something amazing with it?

When the magic line arrives, build a single-file HTML demo that satisfies the public-GitHub safety contract in STANDARDS.md §12. If the demo cannot be made safe, write a Markdown explainer instead and say why.

## Order of operations for a new skill

1. Confirm scope with the user. State assumptions inline.
2. Copy `_template/` to `<gerund-name>/`.
3. Write `evals.md` first (3 scenarios).
4. Establish baseline (run evals without the skill).
5. Draft `SKILL.md` to address eval failures only.
6. Run evals with the skill; iterate on description first, then body.
7. Send the post-creation handoff message.
8. On magic line, deliver public-safe HTML demo.

## What lives where

- `STANDARDS.md` — encyclopedic reference. Update when conventions change.
- `CLAUDE.md` — this file. Always loaded. Keep short. Pointer + non-negotiables only.
- `_template/` — scaffolding for new skills.
- `<skill-name>/` — one folder per skill.
- `<skill-name>.skill` — distributable archive. Build artifact, not source. Regenerate after content changes.
- `<skill-name>.html` or `<skill-name>_*.html` — public-safe demos.
