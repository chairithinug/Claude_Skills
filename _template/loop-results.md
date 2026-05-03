# Trigger eval results — <skill-name>

Lightweight, committed summary of `run_loop.py` runs against this skill's trigger eval. Raw outputs (HTML reports, JSON dumps, candidate-description history) live in `evals/loops/<date>/` and are gitignored. This file is what gets read later.

Each run gets its own dated section appended at the top — newest first.

---

## YYYY-MM-DD (model: <model-id>)

**Eval set used**: `evals/trigger-eval.json` (20 cases, 10 positive / 10 negative — note any modifications since last run)

**Baseline** (current description, before loop ran):
- Train: X.XX
- Test: X.XX
- Trigger rate on positives: XX%
- False-positive rate on negatives: XX%

**Best after N iterations**:
- Train: X.XX
- Test: X.XX
- Iterations run: N (max was 5)
- Convergence: <describe — e.g., "test score plateaued after iteration 3, kept running to confirm">

**Best description suggested**:

> [Paste the best_description here, in full. Keep verbatim so the diff against the current description is clear.]

**Diff against current**:
- <one-line summary of the structural change — e.g., "added 'when the user pastes a long prompt' as an explicit trigger phrase">
- <or "no substantive change — loop converged on what was already there">

**Decision**: ACCEPTED / REJECTED / MODIFIED on YYYY-MM-DD
- *Reason*: <one-line — e.g., "test score improvement +0.07 was real, applied verbatim" or "loop made the description noticeably more aggressive than house style allows; rejected and stayed with current">

**Patterns worth noting**:
- <which negatives consistently fired when they shouldn't have — root cause if known>
- <which positives consistently missed — root cause if known>
- <any cases that flipped between iterations — flag as ambiguous, may be worth rewording the eval query>

**Cost / time**:
- Tokens: ~XXk
- Wall-clock: ~XX minutes
- Cost: ~$X.XX

---

<!-- Append additional dated runs above this line, newest first. Older runs stay in place for archaeology. -->
