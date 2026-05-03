---
name: thai-dish-picking
description: >
  Suggests 3 Thai dish ideas when the user is deciding what to eat — especially
  for lunch in Thailand. Use whenever the user types /thai-dish-picking or
  expresses food indecision in a Thai context with phrases like "what should I
  eat", "lunch ideas", "I'm hungry", "you pick something", "กินอะไรดี",
  "เมนูแนะนำ", "ไม่รู้จะกินอะไร". Also use when the user wants Thai food
  suggestions tuned to their mood, weather, location, dietary needs, budget, or
  what they ate recently. Default to using this skill for any Thai food picker
  / suggester / decision-help request, even when framed casually. Do NOT use
  for restaurant-finding ("where should I eat"), recipe / cooking questions, or
  general overviews of Thai cuisine.
---

# /thai-dish-picking — Thai Dish Suggestions

A skill for suggesting Thai dishes that goes beyond the famous handful everyone already knows. Output is always **3 dishes with quick reasoning each**, intentionally varied so the user has a real choice.

## Core idea

Thai food is genuinely diverse — 4 main regions, hundreds of common dishes, dozens of preparation styles. A naive "suggest a Thai dish" answer collapses to the same handful: pad krapao, pad thai, tom yum kung, green curry, som tam, khao man gai. A good suggestion respects the user's actual context (mood, weather, what they ate yesterday, where they are) and uses the breadth of the cuisine.

Treat the user as someone who lives in Thailand. Skip lengthy "this is a famous Thai noodle dish made with..." preambles. Use Thai script + transliteration first, English gloss only if the dish is obscure or the name doesn't translate cleanly.

## When to use this

- User explicitly types `/thai-dish-picking`
- User expresses food indecision in a Thai context: "what should I eat", "lunch ideas", "I'm hungry", "you pick something", "กินอะไรดี", "เมนูแนะนำ", "ไม่รู้จะกินอะไร"
- User wants Thai food suggestions tuned to their mood, weather, location, dietary needs, budget, or what they ate recently
- User asks the picker question casually mid-conversation — default to firing rather than asking whether they want suggestions

Do NOT trigger for restaurant-finding ("where should I eat"), how-to-cook questions, or general overviews of Thai cuisine — those are different asks.

## Steps / Workflow

### 1. Gather inputs (or infer)

Don't ask for everything — pick at most 1–2 questions that close the most important context gap. If the user just said "what should I eat for lunch", reasonable defaults are fine and the skill can proceed.

Useful axes:
- **Mood / energy** — light vs hearty, spicy vs mild, comfort vs adventurous
- **Weather** — Bangkok-hot favors cold/sour/light dishes; rainy or aircon-cold favors soupy/warm
- **Location** — region of Thailand; type of venue (office food court, street, mall, ข้าวแกง shop, sit-down restaurant)
- **Constraints** — budget, time pressure, dietary (vegetarian, halal, no pork), allergies (peanut, shellfish)
- **Recent meals** — what was eaten yesterday or this morning, to avoid repeating protein/style/region
- **Agency level** — did the user give specifics, or are they saying "you pick"?

If the user gave nothing and explicitly handed over the choice ("you pick", "random", "surprise me"), skip ahead to **Step 4 — Full agency mode** — don't ask questions.

### 2. Research bilingually

Don't rely only on memory. Training data tends to overrepresent the same famous 20 Thai dishes. Research liberally to surface dishes the user might not have thought of — especially regional, seasonal, or shop-specific ones.

**Search bilingually.** English search returns the famous 20. Thai search returns what locals actually eat. Use both.

Useful Thai search terms (mix and match):
- `เมนูข้าว` (rice menu items), `เมนูเส้น` (noodle dishes)
- `อาหารกลางวัน แนะนำ` (recommended lunch food)
- `กินอะไรดี [neighborhood/region]`
- `อาหารใต้` / `อาหารเหนือ` / `อาหารอีสาน` / `อาหารภาคกลาง` (Southern / Northern / Isan / Central)
- `เมนูเด็ด ร้านข้าวแกง` (best dishes at curry-rice shops)
- `อาหารตามสั่ง เมนูแปลก` (less-common stir-fry-to-order items)
- `[dish name] สูตรดั้งเดิม` (to find regional variants of a known dish)

Useful English terms when relevant:
- `regional thai food [region]`
- `thai lunch dishes beyond pad thai`
- `[specific dish name] variants`

Ten searches aren't needed — 2–3 well-chosen queries usually surface enough. Search more if the constraint is unusual (e.g., "vegetarian Southern Thai lunch" needs more digging than "something light for a hot day"). If candidates from memory are already strong and varied, one confirming search is enough.

### 3. Apply diversity rules

The 3 dishes should feel like a real choice, not 3 variations of the same idea.

- **Spread across at least 2 axes**: region (Central / Isan / Northern / Southern), category (rice plate / noodle / soup / curry / salad-yam / one-dish meal / made-to-order), or vibe (light / hearty / spicy / mild / soupy / dry).
- **Avoid the autopilot list** unless the user's constraint genuinely points there: pad krapao, pad thai, khao man gai, tom yum kung, green curry, som tam Thai, massaman, tom kha gai. If two of the 3 picks come from this list, redo the selection.
- **If the user gave a strong constraint** (e.g., "must be noodles"), vary the other axes — different broths, regions, proteins, dry vs soup.
- **Don't repeat the protein** across all 3 picks unless the user asked for it (avoid all chicken or all pork).

### 4. Full agency mode (when the user hands over the choice)

When the user explicitly hands over the choice ("you pick", "random", "surprise me", "ไรก็ได้"):

1. Roll a region. Rough Bangkok-availability weighting: Central ~40%, Isan ~25%, Southern ~20%, Northern ~15%. Adjust if user is elsewhere in Thailand.
2. Roll a category: rice plate, noodle, curry+rice, soup, salad/yam, made-to-order, one-dish meal.
3. If the obvious dish for that region+category is on the autopilot list, consciously consider the second-most-obvious option (e.g., Northern + soup → not just ข้าวซอย khao soi; consider น้ำเงี้ยว nam ngiao or แกงฮังเล gaeng hang lay).
4. Repeat for picks 2 and 3, ensuring no two picks share both region AND category.

The goal of random mode is *genuine* surprise. If all 3 picks would be recognized by a tourist, defaults dominated — try again.

## Output format

Use this shape:

> Based on [1-line summary of context used]:
>
> **1. [Thai script] / [transliteration]** — [English gloss only if non-obvious]
> [1 sentence: what it is, region if non-obvious]
> *Why:* [1 sentence tying it to their input]
>
> **2. ...** (same shape)
>
> **3. ...** (same shape)

Keep each pick to 2–3 lines. The user wants to scan and decide, not read an essay. The user said they'll find the dish themselves, so don't add restaurant or stall recommendations unless they ask.

For full agency mode, drop the "Based on" line and just frame as: "Random pick across regions:" or similar.

No sycophantic opener, no trailing summary.

## Edge cases

**Follow-up: "something else" / "different"**: keep the same constraints, generate 3 fresh picks that don't overlap with the previous set on dish or category.

**Follow-up: "more like #2"**: use #2 as the seed; generate 3 picks in the same region/category/vibe but different dishes.

**Follow-up: "pick one for me"**: choose the one that best matches the stated context (or any if full agency), give a one-line reason.

**User is outside Thailand**: the Bangkok-availability weighting in Step 4 may be off. Adjust toward what's actually available in their location (e.g., diaspora Thai restaurants in the US lean Central + Isan; Northern and Southern dishes are rarer). Mention the limitation if it changes the picks meaningfully.

**Unusual dietary constraint** (vegan, halal, gluten-free, severe peanut/shellfish allergy): research more carefully — the famous 20 mostly fail at least one of these. Lean on `อาหารเจ` (vegetarian/vegan) or halal-specific search terms for Thai-language results.

**User rejects all 3 picks**: ask what specifically didn't fit (region, vibe, protein, novelty level), then regenerate with that constraint added. Don't just re-roll without adjusting.

**User keeps asking with the same constraints across calls**: vary the picks aggressively each time. If the user wants the same kind of dish repeatedly, name it explicitly and ask whether they want a single committed recommendation rather than fresh sets.

**Combined with /deciding** (when available): If the user is genuinely deciding between two specific dishes (not picking from open-ended Thai cuisine), suggest `/deciding` instead — picking has the wrong shape for "Option A vs Option B." If `/deciding` is not in the available skills list, just give a one-line trade-off and let the user choose.

## Reference files

- [`evals/trigger-eval.json`](evals/trigger-eval.json) — 20 trigger test cases (10 should-fire, 10 should-not-fire), mix of English and Thai-script. Negatives test the "NOT for restaurant-finding, recipes, or non-Thai cuisine" rule from the description.

## Worked example

**Example 1 — light constraint on a hot day:**
User: "lunch ideas, something light, it's hot today"

Good picks:
1. ขนมจีนน้ำยา (kanom jeen nam ya) — fermented rice noodles with light fish-curry sauce, served room temp
2. ยำวุ้นเส้น (yam woon sen) — cold glass-noodle salad, sour and refreshing
3. ข้าวแช่ (khao chae) if seasonal — chilled jasmine-water rice with traditional sides

Bad picks (all wrong for the brief): tom yum kung (heavy/hot), green curry (heavy), pad thai (autopilot reach).

**Example 2 — full agency:**
User: "you pick"

Good picks (rolled different regions and categories):
1. ลาบเป็ด (laab ped) — Isan, salad/yam, duck
2. ข้าวคลุกกะปิ (khao kluk kapi) — Central, one-dish meal, shrimp paste rice
3. แกงไตปลา (gaeng tai pla) — Southern, curry, intense fish-innards curry

Bad picks: pad krapao + pad see ew + khao man gai (all Central, all autopilot, all the same vibe).

**Example 3 — strong constraint:**
User: "I want noodles, not pad thai"

Good picks (all noodles, varied on broth/region/style):
1. ก๋วยเตี๋ยวเรือ (kuay tiew reua) — Central, dark beef/pork broth, intense
2. ขนมจีนน้ำเงี้ยว (kanom jeen nam ngiao) — Northern, tomato-pork-blood broth, tangy
3. ผัดซีอิ๊วเส้นใหญ่ (pad see ew sen yai) — Central, dry stir-fry, sweet-savory

Bad picks: 3 variations of pad thai, or 3 different soup noodles from the same region.

## Anti-patterns

- User asks where to eat (restaurant/location query) — answer normally, this isn't picker territory.
- User asks how to cook a dish — answer normally, this isn't picker territory.
- User asks for an overview of a regional cuisine — give an overview, not 3 picks.
- User asks about non-Thai food — answer normally.
- All 3 picks fall into the autopilot list — redo the selection. The whole point of the skill is breadth.
- Restaurant or stall names appear in the output — don't add these unless explicitly asked. The user said they'll find the dish themselves.
