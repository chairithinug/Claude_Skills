# Evals — logistics-advising

Three representative scenarios that test whether this skill solves the gap it was written for. Run these *without* the skill first to establish baseline, then with the skill installed.

Each scenario stresses a different layer of the 6-layer framework so we know the skill isn't only good at one slice.

---

## Eval 1 — Cross-border + finance (Layer 3 + Layer 4 dominant)

**Query**:
> We're a Thai electronics contract manufacturer shipping to a US buyer. Tariffs are eating margin. We've been using FOB Laem Chabang. Buyer is asking us to switch to DDP. Should we?

**Expected behaviors** (skill loaded):
- Names the Incoterm mismatch explicitly: FOB on containerized cargo is technically inappropriate; FCA is the correct ocean-container Incoterm.
- Flags the importer-of-record exposure that DDP creates under a volatile US tariff regime — directional dollar math required, not vibes.
- Sequences advice in priority order: don't accept DDP first; correct Incoterm second; tariff engineering / origin rules third.
- Names at least two failure modes from the Layer 3 list (Incoterm mis-assignment, FTA preference unclaimed, HS classification drift, audit-trail neglect).
- Working-capital impact is shown directionally — DSO extension under DDP should be quantified.
- Open questions force the buyer's underlying ask into the open (single-invoice convenience vs. real control), and probe RCEP cumulation if any inputs are CN/KR/JP.

**Baseline behavior** (skill not loaded):
- Generic Incoterm explanation from a forwarder website. May explain DDP vs FOB definitions correctly but miss the IOR exposure framing, working-capital math, and tariff engineering opportunity. Likely doesn't recommend FCA over FOB. Doesn't sequence by ROI.

**Pass/fail criterion**: Recommendation explicitly warns against accepting DDP without modeling IOR exposure, names FCA as the correct Incoterm for containerized cargo, and shows directional working-capital math.

---

## Eval 2 — Warehouse operations (Layer 2 dominant)

**Query**:
> Our 3PL warehouse pick rate has been declining for 3 months — from 65 lines/hour down to 48. Volume is up 20% over the same period. Boss wants to invest in AMRs. Worth it?

**Input files** (if any):
- None required.

**Expected behaviors** (skill loaded):
- Diagnoses *before* recommending automation: distinguishes symptom (pick rate decline), proximate cause (capacity constraint colliding with volume growth), structural driver (likely slotting decay, labor management gaps, or master-data drift — not necessarily a robotics problem).
- Names the foundation-layer prerequisites for any AMR decision: master-data quality, slotting discipline, current pick path analysis, labor management standards. AMRs amplify good processes and amplify chaos equally.
- References the warehouse-operations failure mode: "automating chaos rather than first cleaning up master data and process."
- Recommends a sequenced approach: slotting/labor diagnostics → process fixes → vendor pilot scoped narrowly → scale.
- Names KPIs to verify after fixes: lines-per-hour, pick accuracy, dock-to-stock, labor-hours per order.
- Loads `references/warehouse-operations.md` and/or `references/vendor-landscape.md` for the AMR vendor reality check.

**Baseline behavior** (skill not loaded):
- Likely jumps to AMR ROI math or a generic "automation transformation" pitch. Misses slotting/labor diagnostics. Doesn't flag the "automating chaos" failure mode.

**Pass/fail criterion**: Output recommends a slotting + labor diagnostic *before* the AMR investment, names the "automating chaos" failure mode, and ties recommendations to specific warehouse KPIs.

---

## Eval 3 — Strategic resilience (Layer 6 + grounding)

**Query**:
> Board is asking whether we should nearshore some of our Asian sourcing to Mexico to reduce US tariff exposure. We're a US consumer electronics brand sourcing about 60% from China currently.

**Expected behaviors** (skill loaded):
- Layer-checks before recommending: this is a Layer 6 (strategic resilience) question with mandatory Layer 3 (FTA / origin rules) and Layer 4 (working-capital + landed-cost) overlay.
- Doesn't treat nearshoring as a yes/no — frames it as a portfolio question (what % of which categories, on what timeline).
- Names the customs/origin trap: USMCA rules of origin require substantial transformation, not just final assembly. Calls out the risk of paying tariff on goods that fail origin verification.
- References at least one canonical failure case from `references/failure-case-library.md` (e.g., the 2011 Thailand floods for sole-source resilience, or the post-2018 China-tariff reshoring wave for the messy reality of nearshoring).
- Quantifies directionally: tariff savings on shifted volume vs. the higher Mexico cost-of-goods + setup capex + working-capital hit during ramp.
- Names failure modes: tariff engineering without origin discipline, automating chaos, vendor-pitched architecture (consultants who promise nearshoring as a silver bullet).
- Open questions: which SKUs, what's the tariff exposure by HS code today, what's the supplier ecosystem look like in Mexico for those categories, what's the BCP plan if Mexico-side disruptions hit.

**Baseline behavior** (skill not loaded):
- Likely produces consultant-deck framing: "diversify sourcing, build resilience, hedge tariff risk." May skip rules-of-origin specifics. Unlikely to ground in canonical failure cases. Probably no directional math.

**Pass/fail criterion**: Output frames nearshoring as a portfolio question (not yes/no), explicitly addresses USMCA rules of origin, references at least one canonical failure case, and provides directional math on tariff savings vs. cost-of-goods + working-capital.

---

## Discovery test (trigger eval — see `evals/trigger-eval.json` for the full set)

Before measuring output quality, confirm the skill triggers at all on a natural-language query:

**Query**: "We're paying duty on goods I'm pretty sure qualify for ATIGA preference but our broker says it's not worth the paperwork. Thoughts?"

**Pass**: Claude reads `SKILL.md` (visible in tool calls).
**Fail**: Claude answers without loading the skill → the description is broken; iterate on it before iterating on the body.
