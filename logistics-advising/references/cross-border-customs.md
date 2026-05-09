# Cross-Border Trade & Customs — Layer 3 Detail

This layer activates whenever goods cross borders. Most international logistics margin is won or lost here.

## Incoterms 2020 (ICC)

11 rules defining responsibility for transport, insurance, customs clearance, and where risk transfers. Updated every ~10 years; previous: Incoterms 2010.

### Multimodal / containerized (use these for containers)
- **EXW** (Ex Works) — seller hands over at premises; buyer does *everything*. Maximum risk for buyer including export clearance. Avoid unless buyer is sophisticated and wants total control.
- **FCA** (Free Carrier) — seller delivers to carrier nominated by buyer at named place. Risk transfers at named place. The correct default for containerized cargo.
- **CPT** (Carriage Paid To) — seller pays carriage to named destination; risk transfers at first carrier.
- **CIP** (Carriage and Insurance Paid To) — same as CPT plus seller-procured all-risk insurance (Institute Cargo Clauses A under Incoterms 2020).
- **DAP** (Delivered at Place) — seller delivers to named destination ready for unloading; buyer clears import.
- **DPU** (Delivered at Place Unloaded) — same as DAP but seller unloads. Replaced DAT in 2020.
- **DDP** (Delivered Duty Paid) — seller delivers to named destination cleared for import. Seller becomes importer-of-record, bears all duties and tariffs. **Use sparingly** — open-ended exposure in volatile tariff regimes.

### Ocean / inland waterway only (legacy; commonly misused for containers)
- **FAS** (Free Alongside Ship) — seller delivers alongside vessel at named port
- **FOB** (Free On Board) — seller delivers on board vessel; risk passes once goods are on board. Still dominant in commodity trade despite being technically inappropriate for containerized cargo (containers are handed over at terminal, not loaded by the shipper)
- **CFR** (Cost and Freight) — seller pays freight to named destination; risk passes on board at origin
- **CIF** (Cost, Insurance, Freight) — same as CFR plus seller-procured insurance (minimum cover Institute Cargo Clauses C under Incoterms 2020 — *not* all-risk)

### Practitioner failure modes
- *FOB used for containerized cargo* — mismatch between physical reality and legal risk transfer; demurrage/detention liability becomes ambiguous. Push to FCA.
- *CIF/CIP insurance scope confusion* — CIF is minimum cover (named perils); CIP under Incoterms 2020 is all-risk. Buyers often assume they have all-risk and discover otherwise after a claim.
- *Named place imprecision* — "FOB Thailand" is meaningless; "FOB Laem Chabang" vs "FOB Bangkok" determines actual risk transfer
- *DDP without tariff hedging* — exporter eats every tariff escalation between order and clearance. Under volatile tariff regimes, DDP is a margin trap.
- *Demurrage/detention liability not allocated* — should be explicit in contract regardless of Incoterm

## HS Classification

The World Customs Organization Harmonized System: 6-digit codes, ~5,400 headings, used by ~200 economies. Extensions:
- **AHTN** (ASEAN Harmonized Tariff Nomenclature) — 8 digits, used across ASEAN
- **Thailand** — 11 digits (AHTN + Thai national subdivisions)
- **HTSUS** (US) — 10 digits
- **EU CN** — 8 digits (Combined Nomenclature)

A misclassification can swing duty 0% ↔ 80% and is the single largest source of avoidable customs penalty exposure.

### Best practice
- Maintain a master HS-code library by SKU; treat as part of master data
- Apply for **Advance Tariff Ruling** (called Advance Customs Ruling in Thailand, Binding Tariff Information in EU, Customs Ruling in US) for ambiguous goods — gives binding pre-clearance certainty for ~3 years
- Periodic compliance audit; HS schedule is updated by WCO every 5 years (latest: 2022 amendments)
- For composite goods, apply the General Interpretive Rules (GIR) — essential character determines classification
- Documentation discipline: technical specifications, BOM, material composition supporting the chosen classification

## Customs Valuation

WTO Valuation Agreement: six-method hierarchy applied in order, no skipping unless prior method fails.

1. **Transaction value** — price actually paid or payable, plus statutory additions (commissions, royalties, assists, packing). Used for ~90%+ of flows.
2. **Transaction value of identical goods**
3. **Transaction value of similar goods**
4. **Deductive value** — resale price working back to import value
5. **Computed value** — production cost + profit + general expenses
6. **Fallback** — reasonable means consistent with the agreement

### Thailand specifics
- Imports valued on **CIF** basis (Cost + Insurance + Freight)
- Duty = CIF × duty rate
- VAT = (CIF + Duty + Excise + other duties) × 7%
- 7% VAT applies from the first baht of import value (post-2024 rule — the previous low-value de minimis no longer applies)
- Excise on alcohol, tobacco, luxury items separately

### Failure modes
- Related-party transactions priced for transfer-pricing purposes but not adjusted to arm's-length for customs — invites both customs and tax audit
- Royalties / license fees not included in dutiable value when condition-of-sale tests met
- "Assists" (free or below-cost tooling, materials, design) not added to value

## Rules of Origin & FTA preferences

The single biggest lever for landed-cost optimization in international trade.

### Origin determination
- **Wholly Obtained (WO)** — grown, mined, born/raised, or fished in the territory
- **Substantial transformation** — three common test types:
  - *Change in Tariff Classification (CTC)* — at heading (CTH), subheading (CTSH), or chapter (CC) level
  - *Regional Value Content (RVC)* — typically ≥40% (build-up or build-down formulas)
  - *Specific Process Rule (SPR)* — defined manufacturing process must occur

### Cumulation
Critical concept: inputs from other FTA members count toward originating value/process.
- **Bilateral cumulation** — inputs from the partner country count
- **Diagonal cumulation** — inputs from a third country in a network of agreements with identical origin rules count
- **Full cumulation** — value-added calculations sum across the FTA region

RCEP (in force Jan 2022) introduced *full cumulation* across ASEAN+5 — a real upgrade vs. the bilateral ASEAN+1 FTAs for products using inputs from multiple regional sources.

### Practitioner workflow
1. Classify goods (HS code)
2. Identify applicable FTAs (often multiple)
3. Determine origin under each FTA's rules
4. Compare landed cost under each preference
5. Choose optimal — generally lowest duty, lowest compliance friction
6. Set up Certificate of Origin issuance (e-Form D for ATIGA, RCEP CoO for RCEP, etc.)

### FTA utilization rates remain unevenly low
Not because preferences are unavailable but because origin documentation isn't set up. The waste shows up as MFN duty paid on goods eligible for 0%.

## Transit, bonded, and special regimes

- **Bonded warehouse** — goods stored under customs control; duty deferred until removal for home consumption. Useful for staging, regional distribution, slow-moving inventory
- **Free Trade Zone / Free Zone / Customs Bonded Area** — designated zones where goods entered without duty; duty triggered only when goods leave for home consumption. In Thailand: BOI Free Zones, IEAT Free Zones, EEC Free Zone
- **Inward processing relief (IPR) / Customs warehouse** — duty exemption or refund on inputs to goods that are subsequently re-exported. Essential for contract manufacturers
- **Duty drawback** — refund of duty paid on inputs incorporated into exported goods
- **ATA Carnet** — temporary admission for samples, professional equipment, exhibitions. ~80 countries accept; 1-year validity; avoids duty/VAT on temporary movements
- **Transit regimes** — TIR Convention (international); ASEAN Customs Transit System (ACTS) for ASEAN overland; GMS CBTA for Mekong region

## AEO — Authorized Economic Operator

WCO SAFE Framework concept: trusted-trader status with reduced inspection rates, expedited clearance, mutual recognition across economies.

- US: C-TPAT (security focus)
- EU: AEO-C (customs simplifications), AEO-S (safety/security), AEO-F (full)
- Thailand: AEO-Importer/Exporter, AEO-Broker (tiered)
- Mutual recognition arrangements progressively negotiated — Thai Customs has MRAs with Korea, Hong Kong; more in progress

Best practice: pursue AEO when import/export volumes justify the compliance investment (~$50K–$200K initial, ongoing audit cost). Payback comes from reduced inspection-related delays.

## Trade Facilitation Agreement (WTO TFA)

Entered into force February 2017. Mandates predictable, transparent customs procedures; advance rulings; release before final duty determination; published timing standards. Implementation status varies by economy; APEC tracks progress through SCFAP III.
