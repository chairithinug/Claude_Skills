# Evals — thai-dish-picking

Three representative scenarios that test whether this skill solves the gap it was written for. Run these *without* the skill first to establish baseline, then with the skill installed.

The skill's load-bearing moves: **3 dishes** (always), **diversity across 2+ axes** (region, category, vibe), **bilingual search** (avoiding the famous-20 autopilot), and Thai script + transliteration first. Failure modes: returning fewer than 3 dishes, all 3 from the autopilot list (pad thai, pad krapao, tom yum, green curry, som tam, khao man gai, massaman, tom kha gai), or relying on memory only without surfacing less-common dishes.

---

## Eval 1 — Light user input (Bangkok lunch, hot day)

**Query**:
> /thai-dish-picking lunch ideas? It's burning hot in Bangkok today.

**Expected behaviors** (skill loaded):
- Researches bilingually — at least one Thai-language search to surface beyond-the-famous-20 candidates.
- Returns exactly 3 dishes.
- Picks favor cold / sour / light dishes given Bangkok-hot weather (e.g., yam wun sen, khao chae if seasonal, tam khao pod, sukiyaki haeng cold version, larb-cool variants).
- Diversity across at least 2 axes — not 3 different yams or 3 different rice plates.
- At most ONE dish from the autopilot list; ideally zero given the weather constraint pulls toward less obvious picks.
- Output uses Thai script + transliteration first; English gloss only when non-obvious.

**Baseline behavior** (skill not loaded):
- Likely returns "som tam, pad thai, tom yum kung" or similar. Three from the autopilot list. No bilingual search. Generic.

**Pass/fail criterion**: Output is exactly 3 dishes, ≤ 1 from the autopilot list, diversity across ≥ 2 axes, Thai script + transliteration on each.

---

## Eval 2 — Constrained input (vegetarian Southern Thai)

**Query**:
> /thai-dish-picking I want to try Southern Thai food but I'm vegetarian. What should I get?

**Expected behaviors** (skill loaded):
- Researches more deeply — vegetarian Southern Thai needs more digging than "something light".
- Returns 3 dishes that are actually vegetarian (not "Southern dish, just hold the fish" — must be authentically meat-free).
- All 3 are Southern (constraint locked) but vary across category (one curry, one stir-fry, one rice plate, etc.).
- Possible candidates: ผัดสะตอ pad sa-tor (vegetarian version), แกงเหลือง gaeng leuang (with vegetables only), ข้าวยำ khao yam (south-style mixed rice with herbs and condiments — naturally vegetarian-adaptable), ผักเหรียง pak liang stir-fry, ผัดเผ็ดเห็ด pad phet hed (Southern-style spicy mushroom).
- Honest about which dishes are commonly vegetarian vs. need substitution; avoids fabricating dishes.

**Baseline behavior** (skill not loaded):
- Likely returns "green curry without chicken" type non-answers, or generic Thai vegetarian dishes (not Southern), or only 1–2 dishes.

**Pass/fail criterion**: Exactly 3 Southern dishes, all genuinely vegetarian (not just adaptable), diversity across category, Thai-script names with transliteration.

---

## Eval 3 — Full agency mode (user hands over the choice)

**Query**:
> /thai-dish-picking just pick something for me, I can't decide

**Expected behaviors** (skill loaded):
- Skips clarifying questions entirely (per workflow Step 4).
- Rolls region + category randomly per the Bangkok-weighting heuristic.
- Picks 3 dishes that don't share both region AND category.
- Avoids the autopilot list — if the obvious dish is on it, consciously picks the second-most-obvious for that region+category.
- All 3 picks should NOT be recognized by a tourist as "Thai's greatest hits" — full agency mode is meant to genuinely surprise.

**Baseline behavior** (skill not loaded):
- Likely returns "pad thai, tom yum, green curry" — the absolute floor of the autopilot list.

**Pass/fail criterion**: Exactly 3 dishes, no two share both region AND category, no more than 1 from the autopilot list (ideally zero), each pick is something a Thai food enthusiast would consider a genuine "good call" rather than tourist defaults.

---

## Discovery test (trigger eval — see `evals/trigger-eval.json` for the full set)

**Query**: "กินอะไรดี"

**Pass**: Claude reads `SKILL.md` and runs the picker.
**Fail**: Claude treats this as a generic chat or asks "what kind of food are you in the mood for?" without invoking the skill — Thai-language trigger phrase isn't firing.
