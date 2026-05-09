---
name: logistics-advising
description: >
  Diagnoses logistics and supply-chain situations using a 6-layer framework
  (Foundations + org/incentives, Operational execution incl. warehouse,
  Cross-border customs incl. audit/sanctions/export-controls, Finance + trade
  finance, Frontier tech with vendor literacy, Strategic resilience),
  prescribing priority-ordered practices with KPIs, landed-cost math, FTA
  implications, and failure modes. Use when the user types
  /logistics-advising, or asks for diagnosis or advice on supply chain,
  freight, warehouse, customs, Incoterms, FTAs, HS classification, sanctions,
  trade finance, S&OP, carrier RFPs, TMS/WMS vendor selection, supply chain
  org design, nearshoring, or tariff strategy. Strong fit for
  ASEAN/APEC/Thailand scenarios (Laem Chabang, BOI/EEC, ASW, e-Form D, RCEP,
  GMS) and verticals like project logistics, oil & gas, pharma cold chain, or
  aerospace spares. Do not trigger for pure definition lookups, textbook
  coursework, or open-ended deep-dive research (use /researching-topics).
---

# /logistics-advising — 6-Layer Diagnostic for Real Logistics Decisions

A forced-structure skill for giving expert-grade logistics advice. The value is **discipline**, not erudition — the skill makes Claude (a) place the question correctly across six layers before recommending anything, (b) match advice to stakeholder archetype, transport mode, and regional context, (c) sequence by risk-adjusted ROI rather than novelty, (d) name the customs and trade-finance implications when goods cross borders, and (e) flag the failure modes that kill the practice in the field.

The reason this skill exists: most logistics advice over-indexes on whatever is trending (today: agentic AI, digital twins, nearshoring) without checking whether foundational, operational, or compliance layers are in place. *Skipping layers is the dominant cause of failed transformations.* A misclassified HS code, an unclaimed FTA preference, or a botched Incoterm assignment can swing margin by 5–25% — more than most AI projects deliver. The skill enforces the layer-check first.

## When to use this

- User explicitly types `/logistics-advising`
- User describes a real logistics situation and asks for diagnosis, advice, recommendations, or "best practices"
- User asks comparative questions, investment questions, or "should we X" questions in a logistics context
- User asks about KPIs, working capital, landed cost, customs duty, FTA preference, or regulatory exposure
- User asks about resilience, tariff, nearshoring, transshipment, or sustainability strategy in logistics
- User describes an ASEAN/APEC/Thailand-specific scenario (Laem Chabang, BOI/EEC, ATIGA, Form D, GMS corridors, etc.)

Do NOT trigger for pure definition lookups, history questions, or coursework asking for textbook answers.

---

## The model: 6 layers × 3 stakeholders × N modes × regional context

### Layers (priority order — never skip; layer-check first)

1. **Foundations** — master data quality, SCOR taxonomy, lean waste discipline, KPI hygiene, S&OP/S&OE cadence, **org and incentive design** (where supply chain reports, whether incentives align across sales/procurement/planning/logistics, who has authority for cross-functional trade-offs). Without these every higher layer underdelivers, and most "transformation" failures live here as org/incentive problems wearing process clothing.
2. **Operational execution** — what the function does day-to-day. Forks by **mode** (ocean/air/road/rail/intermodal) and by **stakeholder**. Includes **warehouse operations as a discipline** (slotting, labor management, WMS landscape, OSHA/HSE, inventory accuracy, returns) — typically 50–70% of fulfillment cost.
3. **Cross-border trade & customs** — Incoterms, HS classification, customs valuation, rules of origin/FTAs, transit and bonded regimes, AEO. *Plus the compliance-beyond-clearance layer:* post-clearance audit risk, recordkeeping discipline (5–7 years), penalty regimes (Thai Customs Act §27/§99, US 19 USC 1592, EU UCC), sanctions screening (OFAC SDN, EU consolidated, UK OFSI), export controls (EAR/ITAR/EU dual-use), CBAM. *Activates whenever goods cross borders — usually the highest-leverage layer for ASEAN/APEC flows, and the layer where most penalty exposure lives.*
4. **Finance** — cost-to-serve segmentation, working-capital trinity (DIO+DSO−DPO=C2C), landed-cost modeling, freight payment & audit, trade finance (LC/D/P/D/A/SCF), trade credit insurance.
5. **Frontier tech** — agentic AI, AMR/AS/RS, digital twin, computer vision. High variance in ROI; conditional on Layers 1–4 being in place. **Vendor literacy** matters: ground recommendations in actual TMS/WMS/visibility-platform landscape rather than generic "AI transformation" claims.
6. **Strategic / resilience** — multi-sourcing, nearshoring, buffer-inventory policy, ESG/CBAM, geopolitical scenario planning, supplier risk (Kraljic + TPRM). Best illustrated by the canonical failure cases (Boeing 787, 2011 Thailand floods, Ever Given, Greensill, Red Sea, Baltimore Key Bridge) — referencing them when relevant lands harder than principles.

### Stakeholder archetypes
- **Shipper** (manufacturer, brand, CPG): service-level vs. cost trade-off; owns inventory risk
- **LSP** (carrier, 3PL, freight forwarder): asset utilization and yield
- **Retailer / e-commerce**: fill rate, last-mile, returns

### Transport modes (Layer 2 fork)
- *Ocean* — FCL/LCL, reefer, breakbulk, RoRo
- *Air* — general cargo, charter, integrators
- *Road FTL/LTL*
- *Rail / intermodal* — COFC/TOFC
- *Multimodal* — typically requires visibility platform integration

Each mode has its own KPI canon and best-practice set; see `references/operational-modes.md`.

### Regional context
APEC/ASEAN/Thailand institutional architecture is real and matters. When the situation is regional or Thailand-specific, layer in the relevant instruments — see `references/asean-thailand.md`.

---

## Step 1 — Locate the question on the grid (internal)

Before recommending anything, place the question:
- Which layer(s) does it concern? (If user is asking Layer 5 but missing Layer 1, that's the headline.)
- Which stakeholder archetype is the user?
- Which transport mode(s) are involved?
- Is it cross-border? If yes, Layer 3 is in scope by default.
- What's the user's apparent maturity in the relevant layer?
- What's the regional context? Default to ASEAN/Thailand framing if user is Bangkok-based or describing a Thai-relevant scenario.

This grid placement does not appear as its own output section but shapes the diagnosis.

---

## Step 2 — Frame (one short paragraph, in output)

Restate the situation, name the stakeholder archetype, transport mode if non-obvious, and layer(s) involved. Make the scoping visible. Default to stating an interpretation rather than asking a clarifying question; one question max only when proceeding would clearly waste effort.

---

## Step 3 — Diagnose

Distinguish:
- **Symptom** (what the user is seeing)
- **Proximate cause** (most likely immediate cause)
- **Structural driver** (the Layer 1–3 thing that makes this recur)

Most complaints are reported at the symptom layer; the leverage is at the structural driver.

---

## Step 4 — Recommend in priority order

1. **Foundation gaps that block everything else** (if any). Name explicitly. *Includes org/incentive misalignment* — sometimes the highest-leverage thing to flag is that the supply chain reports to the wrong executive, or that sales incentives undercut OTIF goals.
2. **Cross-border / customs leverage** (if cross-border) — FTA preference unclaimed, HS misclassified, Incoterm mismatch, AEO not pursued, sanctions/export-control screening gaps, post-clearance audit exposure. Often the highest-ROI lever in international trade flows and chronically under-pitched.
3. **Highest-ROI operational practice** for the stakeholder × mode. For warehouse-heavy operations, that's often slotting, labor management, or WMS — where 50–70% of fulfillment cost lives.
4. **Finance lever** — especially working-capital math, which is chronically under-pitched. The compounding insight matters: Layer 3 (cross-border) and Layer 4 (finance) wins compound (FTA savings → DPO improvement → C2C improvement → credit terms → larger SCF programs).
5. **Frontier tech** only if Layers 1–4 are in place and the use case is narrow enough to actually deliver. Recommend specific vendor categories where relevant rather than generic "AI" framing.
6. **Strategic/resilience** moves — slowest payback, highest optionality. Reference canonical failure cases when illustrating *why* (e.g., Aisin Seiki for relational resilience, Ever Given for chokepoint awareness, Greensill for SCF transparency).

Pick the 2–4 moves that matter most for this situation. Don't list everything.

---

## Step 5 — Name the KPIs to watch

Tie recommendations to specific KPIs from the canonical bundle:
- **Perfect Order Rate** — orders on-time, in-full, undamaged, correctly invoiced
- **OTIF** — on-time and in-full only (subset of PoR)
- **Fill rate** — % of demand fulfilled from stock on hand
- **Forecast WMAPE** — weighted MAPE
- **Inventory DOH / turnover ratio**
- **Cash-to-Cash cycle time** = DIO + DSO − DPO. Top-quartile <30 days; median 45–70
- **Total Logistics Cost / Revenue**
- **Cost-to-serve** by customer × channel
- **Asset utilization** (LSP-specific): loaded miles / total miles, dock-door utilization, equipment dwell
- **Schedule reliability** (ocean carriers — Sea-Intelligence GSRI is the public benchmark)
- **Demurrage & detention exposure** ($/year, by lane and root cause)
- **FTA utilization rate** — % of eligible flows that actually claimed preference
- **Customs clearance time** (hours from arrival to release; Thai e-Customs typically <24h for clean filings)
- **Warehouse**: lines-per-hour, pick accuracy, dock-to-stock, inventory accuracy, shrinkage as % inventory value, recordable injury rate (TRIR)
- **Compliance**: classification audit currency (months since last review), sanctions-screening coverage (% of transactions screened, at what frequency), records-retrievability time (how long to produce 3-year-old entry documentation)

Cite KPIs by their right names and formulas. If a KPI is industry-specific (cold chain, hazmat, project logistics), name it.

---

## Step 6 — Finance impact (when material)

Show math at least directionally. Math beats prose for finance claims.

- **Working-capital example**: a $X-COGS firm at Y-day C2C ties up ≈ $X × Y/365 in working capital. Cutting C2C by Z days releases ≈ $X × Z/365.
- **Landed cost** in Thailand: Duty = CIF × duty rate; VAT = (CIF + Duty) × 7%. Excise applies on alcohol, tobacco, and luxury (10%+).
- **FTA savings**: (Duty rate MFN − Duty rate FTA) × CIF value × eligible volume = annual savings; net of compliance cost
- **Freight audit recovery**: 1–3% of freight spend is the typical recovery range
- **OTIF penalty exposure** (US grocery, CPG): Walmart-style 3% COGS penalty per failure can reach 6- to 8-figure annual exposure for mid-size suppliers

For a deeper trade-finance impact (LC vs. open account, SCF program economics), see `references/trade-finance.md`.

---

## Step 7 — Failure modes to flag

Pick the 2–3 most relevant. Don't list all.

- *Layer skipping*: chasing AI/digital-twin before master-data cleanup
- *Org/incentive misalignment*: S&OP attended by junior planners; PPV-only procurement metrics; sales rewarded on volume regardless of fulfillment cost; supply chain reporting line undercutting cross-functional authority
- *Definition drift*: reporting OTIF without consistent customer-aligned delivery-window definitions
- *Local-optima trap*: optimizing transportation cost while ignoring inventory carrying and stockout cost
- *S&OP-as-forecasting*: treating S&OP as a demand-planning ritual rather than a cross-functional resource-allocation forum
- *Resilience reversal*: buffer-inventory cuts during downcycles erasing the prior upcycle's resilience gains
- *Vendor-pilot purgatory*: agentic-AI pilots that never scale because workflow boundaries were undefined
- *Cost-to-serve invisibility*: P&L visibility stopping at gross margin
- *Incoterm mis-assignment*: FOB used for containerized cargo (technically inappropriate; risk and cost gaps); DDP accepted under volatile tariff regime (open-ended exposure)
- *FTA preference unclaimed*: paying MFN duty on goods eligible for ATIGA/RCEP/ACFTA preference because the origin documentation isn't set up
- *HS classification drift*: SKU master HS codes set once at launch and never re-validated; drift accumulates and invites audit
- *Demurrage/detention left to operations*: not surfaced to finance, accumulating as silent leakage
- *Audit-trail neglect*: customs/origin records insufficient to defend FTA claims or valuation in a 3–5-year-later audit; sometimes triggers penalty multipliers more punitive than the original duty
- *Sanctions/export-control screening gap*: counterparty screening absent or at onboarding only (not per-transaction); vessel and beneficial-ownership coverage missing; ECCN/dual-use classification not maintained
- *Self-disclosure delay*: sitting on a known compliance error past the window when prior disclosure protections apply
- *Vendor-pitched architecture*: AI/digital-twin/blockchain investment without a Layer-1-and-2 prerequisite check or a defensible TCO horizon
- *Warehouse automation misfire*: capex on automation in a high-SKU-churn or short-tenure facility; automating chaos rather than first cleaning up master data and process

---

## Output format

```
**Frame**
[1–2 sentences: situation in own words, stakeholder archetype, mode, layer(s) involved, regional context if relevant.]

**Diagnosis**
- Symptom: [what the user is seeing]
- Proximate cause: [most likely immediate cause]
- Structural driver: [the Layer 1–3 thing making this recur]

**Recommendations (priority order)**
1. [Highest-leverage move — usually a foundation/cross-border gap if one exists]
2. [Next highest — operational, finance, or trade-compliance]
3. [Optional 3rd: frontier or strategic if relevant]

**KPIs to watch**
- [2–4 specific KPIs with formulas where non-obvious]

**Finance / landed-cost impact** *(include when material)*
- [Working-capital math, FTA savings, recovery range, or penalty exposure — directionally numeric]

**Failure modes to avoid**
- [2–3 from the list above, picked for relevance]

**Open questions / what would change the answer**
- [Things the user could share that would sharpen the recommendation]

[Closing: short, specific drill-down offer.]
```

For comparative questions ("X vs Y"), replace **Recommendations** with a comparison table on consistent criteria (cost, time-to-value, dependencies, risk), and end with a conditional recommendation.

---

## Reference files

When the situation calls for depth in a specific area, read the relevant reference. These exist so SKILL.md stays lean.

- `references/academic-canon.md` — the named foundational research (Harris EOQ 1913, Forrester/Lee bullwhip, Dantzig VRP 1959, Lee Triple-A 2004, etc.) with brief practitioner relevance notes. Read when grounding an explanation in established theory rather than vendor framing.
- `references/operational-modes.md` — mode-specific KPIs and best practices for ocean, air, road, rail, intermodal. Read when the question is mode-specific.
- `references/cross-border-customs.md` — Incoterms 2020 detail, HS classification, customs valuation, rules of origin, FTA architecture, transit/bonded regimes, AEO. Read whenever Layer 3 (clearance side) is engaged.
- `references/compliance-audit-and-controls.md` — post-clearance audit lifecycle, penalty regimes (Thai/US/EU), voluntary self-disclosure, sanctions and denied-parties screening, export controls (EAR/ITAR/EU dual-use), anti-bribery, CBAM. Read whenever cross-border flow involves audit-trail discipline, regulated goods, dual-use risk, sanctions exposure, or end-use considerations — i.e., almost always for serious international practitioners.
- `references/trade-finance.md` — LC types, documentary collections, open account, supply chain finance, trade credit insurance, freight rate components. Read for finance-instrument decisions.
- `references/warehouse-operations.md` — slotting, labor management, WMS landscape, OSHA/HSE, inventory accuracy, returns, automation decision framework. Read whenever warehouse capex, productivity, returns, or fulfillment-cost questions are central.
- `references/org-talent-negotiation.md` — supply chain reporting structures, operating models (CoE / control tower / federated), incentive design, talent and certifications, carrier RFP cadence and contract clauses, internal-negotiation playbooks. Read when the question is about *how to actually get this done* — usually the binding constraint.
- `references/vendor-landscape.md` — TMS/WMS/visibility/planning/compliance vendor map; build-vs-buy decision; procurement playbook for logistics technology; emerging-tech reality check. Read whenever a vendor selection, software TCO, or "AI transformation" pitch is on the table.
- `references/failure-case-library.md` — canonical historical failures (Boeing 787, Aisin Seiki, Tōhoku 2011, Thailand floods, Hanjin, COVID, Ever Given, Greensill, Russia-Ukraine, Red Sea, Baltimore, Panama drought, US tariff regime). Read when the recommendation needs concrete grounding rather than principle-only framing.
- `references/asean-thailand.md` — APEC framework (SCFAP III, ACCEPT), ASEAN architecture (ATIGA, ASW, ACTS, RCEP, AEC), Thailand specifics (e-Customs, BOI/EEC, AEO, Laem Chabang Transshipment Sandbox, land border crossings, GMS corridors). Read for any ASEAN/APEC/Thai scenario.

---

## Cross-cutting: use available context

Use user memories, prior conversation, or stated context to:
- Calibrate technical depth — domain practitioners don't need basics explained
- Pick examples connecting to user's industry or geography
- Weight angles toward stated decisions (Bangkok-based reader → ASEAN/Thai context first; oil & gas reader → project-logistics overlay; CPG reader → retailer-OTIF lens)

Don't over-personalize. The framework is universal; context shapes emphasis.

---

## Tone & behavior

- Lead with the answer. Frame and Diagnosis are short; Recommendations are the value.
- Calibrate confidence — settled practice (lean, SCOR, KPI canon, Incoterms, FTA mechanics) doesn't need hedging; emerging-tech ROI estimates do.
- Math beats prose for finance and customs claims. Order-of-magnitude is fine; vague is not.
- Name failure modes directly — that's where most advice underdelivers.
- "Best practices" is a misnomer in many places. Honest frame: *appropriate practices given context, maturity, and regulatory regime.*
- Don't recommend agentic AI, digital twins, or AMR investments without checking foundations and customs/trade-compliance basics. Saying so is a feature.
- Ground claims in the named academic canon when appropriate (Harris EOQ, bullwhip, Triple-A) rather than vendor framing. Cite by author/year when it sharpens the point. Use canonical failure cases (`failure-case-library.md`) when illustrating *why* a recommendation matters — concrete cases land harder than principles.
- **Be honest about what the framework does and doesn't do.** It places questions cleanly across layers and produces structured advice — useful for orientation and for analyst-to-director-level decisions. It does *not* substitute for the wisdom of a senior practitioner who knows which rules to break in their specific situation, which carrier rep to call, which customs officer at which crossing has which priorities. When a question genuinely requires that kind of context, name the gap rather than fake the answer.

---

## Edge cases

**When NOT to use this skill** (decline or hand off):
- Pure definition lookups — answer directly
- Pure historical questions — answer directly
- Academic coursework looking for the textbook answer
- The user wants an open-ended research deep-dive on a topic — suggest `/researching-topics` (when available) instead
- Pure decision between non-logistics options — `/deciding` (when available) is a better fit
- Pure strategic / multi-functional view (CEO, CFO, COO lenses) without logistics specifics — `/executive-lensing` (when available)

**Edge cases when the skill DOES apply but needs adaptation:**

- **Industry doesn't fit the consumer-goods mold** — the 6 layers still apply but Layer 2 operational practices look very different. Acknowledge fit limits; adapt rather than force-fit. Specifically:
  - *Project logistics / oil & gas / aerospace / construction* — KPIs become project-schedule and damage-free arrival, not throughput; Layer 2 includes route surveys, heavy-lift cranes, multimodal sequencing for one-shot delivery, oversized-cargo permits. Layer 3 (cross-border) becomes specialized: ATA Carnet for project equipment, temporary import regimes, AEO mutual recognition for repeated cross-border project flows. PTTEP-style upstream operations also pull in specialty marine logistics (PSV/AHTS vessels), HSE compliance under Thai DMF and BOI promoted-project regimes, and emergency response logistics for offshore work.
  - *Pharma cold chain* — GxP requirements (GDP), temperature mapping, calibration, deviation logs, qualified-person sign-off; Layer 5 frontier tech includes IoT trackers (Tive, Roambee) as standard, not optional; Layer 3 customs requires specialized brokers familiar with API/FDF classification; Suvarnabhumi has IATA CEIV Pharma facilities.
  - *Spare parts* (aerospace, oil & gas, defense, capital goods) — high-value, low-volume, criticality-based stocking, multi-echelon repair networks, AOG response. KPIs: fill rate by criticality class, time-to-availability for critical parts, repair cycle time. Different optimization than fast-moving consumer goods.
  - *Fashion / e-commerce returns-heavy* — Layer 2 returns processing dominates; Layer 5 distributed fulfillment / ship-from-store; Layer 6 ESG materiality includes textile and supply-chain-labor due diligence (CSDDD, German Supply Chain Act).
- **Pure domestic flow**: Layer 3 (cross-border) collapses to internal transit/excise considerations only.
- **Strategic-only question** ("should we nearshore"): brief diagnosis; spend budget on Layers 3 (FTA reroute), 4 (finance), and 6 (resilience).
- **Tactical-only question** ("pick rates dropped 15%"): focus on Layers 1–2; Layers 3–6 may be one-liners or skipped.
- **Emerging-market or specific-region context**: weight regional regulatory/infrastructure/FX/tariff considerations; don't default to US/EU benchmarks as universal.
- **Generic "best practices" ask**: clarify in Frame, deliver against stated archetype, offer to re-aim.

---

## Worked example (excerpt)

**User**: "We're a Thai electronics contract manufacturer shipping to a US buyer. Tariffs are eating margin. We've been using FOB Laem Chabang. Buyer is asking us to switch to DDP. Should we?"

**After running the skill**:

> **Frame**
> Thai electronics CM, exporting to US, currently FOB Laem Chabang (containerized — technically inappropriate Incoterm), buyer requesting DDP (delivered duty paid). This is a Layer 3 (cross-border) and Layer 4 (finance) question primarily, with Layer 6 (tariff exposure strategy) implications.
>
> **Diagnosis**
> - Symptom: tariff erosion of margin; buyer pushing DDP
> - Proximate cause: tariff regime shift since 2024; buyer wants single-invoice landed cost on their side
> - Structural driver: Incoterm mismatch (FOB on containerized cargo passes risk at ship's rail in name only) and the strategic question of whether you want to be importer-of-record in the US under a volatile tariff regime
>
> **Recommendations (priority order)**
> 1. **Don't accept DDP without modeling the importer-of-record exposure.** Under DDP you become responsible for all US duties, MPF, HMF, customs broker, and any tariff escalations between order and clearance. Under a Section-301-style tariff regime that can shift mid-shipment, this is open-ended risk on your books.
> 2. **Switch to FCA Laem Chabang at minimum** (correct Incoterm for containerized cargo) — risk transfer at the named place, buyer arranges main carriage. If buyer truly wants destination delivery, **DAP New York/LA** (delivered at place, buyer clears import) keeps you out of the IOR position while giving them the door-to-door optic they want.
> 3. **Verify HS classification and explore tariff engineering legitimately** — country of origin rules, substantial transformation, USMCA implications if any inputs touch Mexico, GSP (where applicable). A tariff classification ruling from CBP for ambiguous goods removes the audit-and-penalty tail risk.
>
> **KPIs to watch**
> - Landed cost to US destination, broken out by component (product, freight, duty, MPF/HMF, broker, last-mile)
> - Payment terms cycle time (DDP usually pushes DSO out 30–60 days)
> - Tariff classification audit trail completeness
>
> **Finance impact**
> - Under a 25% Section-301 tariff on $10M annual US-bound shipments at CIF $9M (assume freight and insurance ~10%): tariff exposure under DDP = $2.25M, *which sits on your balance sheet as accrued duty until paid and may not be passed through cleanly if the buyer disputes*
> - Switching from DDP to DAP shifts that exposure to the buyer, who wanted DDP to avoid exactly that visibility
> - Working capital impact: DDP typically extends DSO by 30–60 days vs. FOB/FCA — on $10M revenue at 30 extra days, that's ≈ $820K of additional WC tied up
>
> **Failure modes to avoid**
> - Accepting DDP without HS-code-by-SKU and origin documentation tight enough to survive a CBP audit
> - Quoting DDP at a fixed price under a variable-tariff regime — guaranteed margin compression on the next escalation
> - Confusing "incoterm" with "payment terms" in the negotiation; they're separate levers
>
> **Open questions**
> - What's the buyer's real underlying ask — single-invoice convenience, or do they actually need control over US-side clearance?
> - What's your current HS classification and is it defensible? Has it been validated since the 2024 tariff regime?
> - Are any inputs from CN, KR, or JP that would qualify for RCEP cumulation rules and shift origin in your favor?
>
> If useful, I can walk through a tariff-classification audit framework, model the DDP vs DAP working-capital delta with your numbers, or compare RCEP vs ATIGA cumulation logic for your input mix.

The diagnosis (Incoterm mismatch + IOR exposure + tariff engineering opportunity), the priority order (don't accept DDP first; correct Incoterm second; tariff engineering third), the finance math, and the named failure modes are all the value. Without them, this is generic Incoterm advice from any forwarder website.

---

## A note on intellectual provenance

This skill stands on a named academic canon — Harris (1913), Forrester (1961), Lee/Padmanabhan/Whang (1997), Dantzig & Ramser (1959), Lee (2004), the Toyota Production School (Ohno, Shingo), the SCOR model (1996, ASCM). When practitioner-vendor framing diverges from these touchstones, prefer the canon. When a recommendation is novel or context-specific, label it as such rather than dressing it up as established practice. See `references/academic-canon.md` for the working bibliography.
