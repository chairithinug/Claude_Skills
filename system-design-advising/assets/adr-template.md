# ADR-NNNN: [Short Title of the Decision]

**Status**: Proposed | Accepted | Deprecated | Superseded by ADR-XXXX
**Date**: YYYY-MM-DD
**Deciders**: [names or roles]
**Tags**: [e.g., data-layer, api, security]

---

## Context

What problem are we solving? What constraints are in play? What forces (technical, business, organizational) bear on this decision?

Keep this short — 2-3 paragraphs. The reader needs enough context to understand why a decision was needed; they don't need the full history of the system.

## Decision

What did we decide? State it as plainly and unambiguously as possible.

## Considered alternatives

Brief list of alternatives that were considered and why they were not chosen.

- **Alternative A**: [description] — rejected because [reason]
- **Alternative B**: [description] — rejected because [reason]
- **Alternative C**: [description] — rejected because [reason]

## Consequences

What does this decision cost us? What does it buy us?

**Positive**:
- ...
- ...

**Negative**:
- ...
- ...

**Neutral / future implications**:
- ...
- ...

## Flip conditions

Under what circumstances would this decision need to be revisited?

- If [condition X], reconsider — this decision assumed [Y]
- If [scale Z] is reached, the trade-off changes

## References

- [Links to design docs, RFCs, prior ADRs, external articles]

---

## Notes on using this template

- Keep ADRs short (1-2 pages). Long ADRs don't get read.
- Number them sequentially (ADR-0001, ADR-0002…) and store in `docs/adr/` in the repo.
- "Superseded by" creates a chain — old ADRs aren't deleted, they're marked superseded.
- Write the ADR *before* the change ships if possible. Future-you will thank past-you.
- The "Flip conditions" section is unusual but high-value: it tells future maintainers when this decision should be re-examined.
