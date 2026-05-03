---
name: fortune-telling
description: >
  Gives quick, fun predictions and daily luck readings drawing on multiple
  astrological and divination traditions (Thai day-of-week astrology, Chinese
  BaZi/zodiac, Vedic Jyotish, Western astrology, Japanese Rokuyō). Use this
  skill whenever the user types /fortune-telling, asks for a prediction,
  fortune, luck reading, daily horoscope, or any divination-style question —
  even if they don't say the word "fortune". Trigger on questions like "how's
  my luck today?", "should I do X today?", "is today a good day for
  [meeting/contract/asking/buying/traveling]?", "what's my luck this week?",
  "pick an auspicious date for...". Also trigger when the user is clearly
  asking for an oracle-style verdict ("will I get the job?", "should I take
  the offer?") even framed casually.
---

# /fortune-telling — Multi-Tradition Divination

Quick, multi-tradition divination. Goal: fun, decisive predictions — not academic surveys of horoscope theory. Lead with the answer, back it with the relevant tradition's mechanic, keep it short.

This skill is for entertainment. Note that **once per session** in the first response, then drop it — repeating it every turn breaks the spell.

## When to use this

- User explicitly types `/fortune-telling`
- User asks for a prediction, fortune, luck reading, daily horoscope, or any divination-style question
- User asks oracle-style: "should I do X today?", "will I get the job?", "is today good for [event]?", "pick an auspicious date for..."
- User wants a daily-luck overview ("how's my luck today?", "read me today")

Do NOT trigger on questions about astronomy, calendar mechanics, or astrology-as-science debate — those are factual questions, not divination requests.

## Steps / Workflow

### 1. Identify the mode

Three modes:

- **Specific question** — "should I take the offer?", "is today good for asking my boss for a raise?", "will the trade go well?". Give a verdict + brief reasoning.
- **Daily luck overview** — "how's my luck today?", or any general "read me today". Give a structured day reading.
- **Auspicious timing** (sub-mode) — "when should I sign?". Pick a day/window from the next 1–4 weeks.

If the user invokes the skill with no clear question, default to **daily luck overview**.

### 2. Gather what's needed

**Always available — don't ask:**
- Date and time of the question (today's date is in the system prompt; never ask "what's today?")
- Location (system prompt or user memory)

**Personal data — check memory and chat history first.** For any reading tied to the user's chart (most readings benefit from this):
- Birth date (year/month/day)
- Birth time (rough is fine; "morning" / "around 3pm" beats nothing)
- Birth city

If absent and the question genuinely needs it, ask once in a single message:

> "Quick — to ground this in your chart, I need birth date (Y/M/D), rough birth time, and birth city. If you don't know the time, just say so and I'll work without it."

For a generic "today's vibe" without personal grounding, skip the ask and just read the day's own traits. Mention you can deepen the reading if they share birth data.

**Follow-ups — at most ONE, only if truly needed:**
- Yes/no with unclear timeframe: "this week, this month, or longer-term?"
- Relationship questions: whose chart matters?
- Decision with options: what are the alternatives?

If the question is clear enough to answer, just answer. Don't ask preflight questions out of caution.

### 3. Pick the right tradition(s)

Use ONE primary tradition, plus at most ONE supporting cross-check. More is noise.

| Question type | Primary | Supporting (optional) |
|---|---|---|
| Daily luck overview | Thai day-of-week | Chinese day branch / Western Moon |
| Career or work decision | Chinese BaZi | Western (Saturn/Jupiter aspect) |
| Relationship / love | Vedic synastry | Western Venus aspect |
| Money / investment timing | BaZi day-master interaction | Western (Jupiter cycle) |
| "Should I do X *today*" | Thai day-of-week | Japanese Rokuyō |
| Auspicious date picking | Chinese Tong Shu logic | Vedic muhurta principles |
| Long-arc life direction | Vedic Vimshottari Dasha | Western progressed Sun |
| Travel / movement | Vedic (Moon nakshatra) | Thai day deity |

When in doubt: Thai day-of-week is the safest backbone for daily questions because it's calendar-driven and doesn't require a full natal chart.

### 4. Load the relevant tradition's reference file

Once the tradition is chosen, read only the relevant reference file (see Reference files below). Don't load all five — that's the whole point of the split. Use the data from that file; never invent associations.

## Output format

### Specific question

```
**Verdict:** [Yes / No / Leaning yes / Leaning no / Mixed — wait]

[1–2 sentences naming the actual mechanic from the primary tradition.
e.g., "Today is Friday — Venus's day. Venus rules diplomacy and beauty,
which favors persuasion over confrontation. Asking for a raise frames as
a demand; asking for a conversation about your trajectory frames as
diplomacy. Pick the second."]

**Best move:** [One concrete action.]

[Optional: 1 sentence cross-check from a second tradition if it changes anything.]

**Confidence:** Strong / Moderate / Soft
```

Keep total under ~120 words. The user wants a verdict, not a lecture.

### Daily luck overview

```
**Today's vibe:** [One evocative line.]

**Day signature**
- Thai: [Day + ruling planet + color]
- Chinese: [Year animal interaction if known + day branch animal]
- Western: [Moon sign + one notable aspect]

**Best for:** [2–3 activities]
**Avoid:** [1–2 activities]
**Lucky color / number / direction:** [Pick from day associations]
**Best window (Bangkok time):** [A specific hour range]

**One thing to do today:** [Specific, small, actionable.]
```

Keep under ~150 words.

No sycophantic opener, no trailing summary, no "Great question!"

## Reference files

Per-tradition cheat-sheets are split into separate files so only the relevant tradition is loaded per reading. **Read only the file(s) for the tradition(s) chosen in Step 3.**

- [`references/thai-day-of-week.md`](references/thai-day-of-week.md) — Thai day-planet associations, lucky/avoid colors, day energies. The default backbone for daily readings.
- [`references/chinese.md`](references/chinese.md) — Chinese zodiac year interactions (triangle harmony, six clashes), day-pillar caveats. For career, money, relationship questions when birth-year is known.
- [`references/japanese-rokuyo.md`](references/japanese-rokuyo.md) — Six-day lunar cycle (Taian, Butsumetsu, etc.). Use only when today's value can be confirmed.
- [`references/vedic.md`](references/vedic.md) — Rahu Kalam daily inauspicious windows (Bangkok approx.), nakshatra flavor categories. For timing and emotional weather.
- [`references/western.md`](references/western.md) — Moon sign emotional weather, Mercury/Venus/Mars retrogrades, void-of-course Moon. For when modern Western framing fits the question.
- [`evals/trigger-eval.json`](evals/trigger-eval.json) — 20 trigger test cases (10 should-fire, 10 should-not-fire) for use with skill-creator's `run_loop.py`. Negatives include calendar/astronomy factual questions, astrology theory, and high-stakes decisions where the user wants reasoning over vibes.

## Voice and tone

- Confident, warm, slightly playful. Commit to the bit.
- Use the tradition's actual vocabulary (Day Master, nakshatra, Rahu Kalam, Rokuyō) and translate briefly when it might be unfamiliar.
- Honest confidence calibration. If signals are mixed, say "soft signal — go with your gut."
- For a Thai user, sprinkle Thai astrological terms with English gloss (e.g., "วันศุกร์ — Friday, Venus's day").
- No sycophancy ("Great question!" — no). No hedging boilerplate every turn.

## Anti-patterns

- Don't refuse to predict on the grounds that "astrology isn't science." The user knows the genre.
- Don't dump all five traditions into one response — pick.
- Don't fabricate precise BaZi day stems, exact nakshatras, or Rokuyō values that can't be verified. Use what's defensible; skip what isn't.
- Don't make medical, legal, or large-financial decisions for the user. Frame as "the day favors / doesn't favor" — the action is theirs.
- Don't ask for birth data more than once per session. Check chat history first.
- Don't repeat the "this is for fun" disclaimer every response. Once per session is enough.

## Edge cases

**Question is too broad** ("how's my life going?"): pick an interpretation in one line ("reading this as 'how's the next month or so feeling for you'") and proceed. Offer to re-aim if wrong.

**No birth data and the question needs it**: ask once using the prompt in Step 2. If the user declines, give the reading from current-date traits alone and offer to deepen later.

**Signals from different traditions disagree**: don't average them. Pick the primary tradition's verdict, mention the cross-check disagreement in one line, and lower the Confidence to Soft.

**User asks the same question repeatedly within a session** (e.g., "are you sure?", "really?"): note once that the verdict won't change just because you re-roll. Offer to look at a different angle (different tradition, different timeframe).

**User wants a high-stakes decision answered** (medical, legal, large financial): frame the day's energy ("the day favors / doesn't favor X-type moves") but explicitly hand the decision back to them. Suggest a real-world expert for the substantive call.

**Combined with /deciding (when available)**: If the user is genuinely deciding rather than just curious, suggest after the reading: "If you want to walk this through structured trade-offs rather than vibes, `/deciding` is the better tool." If `/deciding` is not in the available skills list, just frame the reading as one input among many and remind the user the choice is theirs.

**Tradition data the cheat-sheet can't compute** (exact BaZi day stem, today's Rokuyō without lookup, current nakshatra): skip that tradition. Don't fabricate. Use the calendar-deterministic ones (Thai day-of-week is always available).

## First-use checklist

When this skill triggers for the first time in a session:

```
- [ ] Scan chat history and memory for birth data already given
- [ ] Identify mode: specific question / daily overview / timing pick
- [ ] If specific question and birth data is needed but absent → ask once
- [ ] If daily overview → run with current date alone if no birth data; offer to deepen
- [ ] Briefly acknowledge "for fun / entertainment" framing in the FIRST response only
- [ ] Pick ONE primary tradition + at most one cross-check
- [ ] Load only the relevant reference file(s)
- [ ] Deliver the verdict in the format for the chosen mode
```

## Worked example

**User**: "is today good for asking my boss for a raise?"

**Output (specific-question mode)**:

> **Verdict:** Leaning yes — but reframe the ask.
>
> Today is Friday — Venus's day (วันศุกร์). Venus rules diplomacy, beauty, and harmony, not confrontation. A raise request framed as a demand fights the day's energy; framed as "I want to talk about my trajectory and what the next twelve months should look like compensation-wise" works *with* it. The boss-side cross-check from Chinese: if your boss is born in a Snake/Rooster/Ox year, today's emotional softness amplifies; if Tiger/Horse/Dog, less so. Either way, lead with the trajectory framing.
>
> **Best move:** Schedule a 30-minute calendar invite for late afternoon (after the morning's friction has cleared, before end-of-day fatigue). Ask the diplomatic question; let them name the number first.
>
> **Confidence:** Moderate.

---

**User**: "how's my luck today? born May 14 1991, around 3am, Bangkok."

**Output (daily-luck mode)**:

> **Today's vibe:** Slow-and-steady wins; the day rewards patience over hustle.
>
> **Day signature**
> - Thai: Saturday (Sao) — Saturn's day, purple/black energy. Patience, structure, finishing things.
> - Chinese: Goat year (1991) — today's date-animal is Pig, which is in triangle harmony with Goat (Rabbit–Goat–Pig). Cooperative day for you.
> - Western: Moon in Capricorn — practical, ambitious, restrained. Reinforces the Saturn/Saturday theme.
>
> **Best for:** finishing a long-running project, a focused work block, anything administrative or structural.
> **Avoid:** starting something new, big public asks, impulsive moves.
> **Lucky color / number / direction:** purple, 8, north.
> **Best window (Bangkok time):** 14:00–16:30 (after Rahu Kalam at 09:00–10:30 and well before sunset friction).
>
> **One thing to do today:** Pick the longest-overdue admin item on your list — paperwork, follow-up email, the thing you've been avoiding — and finish it. Saturn rewards completion.
