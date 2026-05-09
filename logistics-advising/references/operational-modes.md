# Operational Best Practices by Transport Mode — Layer 2 Detail

Each mode has its own KPI canon, contract structure, and failure modes. Read when the question is mode-specific.

## Ocean

The dominant mode for international long-haul (~80% of global trade by volume). Two main service types:

- **FCL** (Full Container Load) — shipper books a whole container (20'/40'/40HC/45'); typical for >12–15 CBM
- **LCL** (Less than Container Load) — consolidated load with other shippers; cost per CBM higher; cycle time longer (deconsolidation step)

### Equipment types
- Standard dry containers (20'/40'/40HC)
- Reefer (temperature-controlled) — pharma, food, chemicals
- Open top, flat rack — out-of-gauge cargo
- Tank containers — liquids, gases
- Breakbulk / project cargo — non-containerizable; chartered vessels
- RoRo (Roll-on/Roll-off) — vehicles

### Carrier landscape
- Major alliances: 2M (Maersk + MSC, dissolving into separate strategies), Ocean Alliance (CMA CGM, COSCO, OOCL, Evergreen), THE Alliance (Hapag-Lloyd, ONE, HMM, Yang Ming) — alliance reshuffling 2025–2026 with Maersk-Hapag "Gemini Cooperation"
- Top carriers by capacity: MSC, Maersk, CMA CGM, COSCO, Hapag-Lloyd, ONE, Evergreen, HMM, Yang Ming, ZIM

### KPIs
- **Schedule reliability** — Sea-Intelligence Global Schedule Reliability Index (GSRI) is the public benchmark; pre-COVID norm ~75–80%, dropped to ~30–40% during 2021–2022, recovering since
- **Transit time** vs. port-pair benchmarks
- **Demurrage & detention** exposure (see trade-finance.md)
- **Container utilization** (CBM filled / capacity)
- **Empty repositioning cost** as % of revenue (carrier-side KPI)

### Best practices
- Hybrid contract / spot mix (60–80% / 20–40%); long-term contract for committed volume on core lanes, spot for peak overflow
- Multi-carrier on critical lanes (avoid alliance concentration risk)
- BAF/CAF formula transparency in contracts; consider fixed-rate clauses on volatile bunker periods
- Negotiate free-time terms (demurrage/detention) — carriers extend when volume justifies
- Schedule integrity service from major carriers (premium product) on time-critical lanes
- Visibility platform integration (project44, FourKites, Wakeo) for predictive ETAs

### Failure modes
- Single-alliance dependence — disruption in 2024 Red Sea showed concentration risk
- "FOB Thailand" without a named port — meaningless under Incoterms 2020
- Demurrage/detention treated as operational expense rather than negotiable contract term

## Air

The mode for time-sensitive, high-value, or perishable cargo. ~1% of global trade by volume but ~35% by value.

### Service types
- **General cargo** via passenger belly capacity
- **Freighter** via dedicated cargo aircraft (B777F, B747F, A330F)
- **Charter** for outsized or time-critical project cargo
- **Integrators** (FedEx, UPS, DHL Express, TNT) — door-to-door express service with own networks

### KPIs
- **Kilo-rate** (USD/kg)
- **Chargeable weight** = max(actual weight, volumetric weight); volumetric divisor is 6000 cu cm/kg for IATA standard
- **On-time uplift** — booked shipment actually flying on booked flight
- **Damage and pilferage rate** — air handling has more touchpoints; damage exposure higher than perception suggests
- **Recovery time** (post-disruption)

### Best practices
- Negotiate lane-specific rates with GSAs (General Sales Agents) and carriers, not just integrators
- Density discipline — air rates penalize low-density cargo heavily
- Pre-build skids/ULDs (Unit Load Devices) for repeat lanes — saves handling time and damage exposure
- Cold chain capability assessment for pharma — IATA CEIV Pharma certification; Suvarnabhumi has CEIV Pharma facilities
- DGR (Dangerous Goods Regulations, IATA) discipline — declarant training, current DGR edition (annual update)

### Failure modes
- Volumetric weight surprises — under-density cargo costs much more per kg of value than expected
- DG declaration errors — substantial fines and shipment holds; no shortcuts on declarant qualification

## Road FTL/LTL

Domestic and regional cross-border.

### Service types
- **FTL** (Full Truckload) — exclusive use of trailer; 24–48ft typical
- **LTL** (Less than Truckload) — consolidated freight, terminal-to-terminal; longer transit time
- **Cross-border trucking** — bonded transit, multiple jurisdictions; in ASEAN, GMS CBTA / ACTS regimes apply
- **Drayage** — port-to-warehouse or warehouse-to-rail-ramp short hauls

### KPIs
- **On-time pickup / delivery** — both matter; pickup misses cascade
- **Claims ratio** — value of claims / total freight billed
- **Loaded miles / total miles** — carrier-side asset utilization
- **Detention** — driver waiting at shipper/consignee dock beyond free time (typically 2 hours free, $50–$75/hr after)
- **Fuel surcharge** — typically indexed to DOE diesel price (US) or equivalent local index

### Best practices
- Hybrid contract (annual RFP) plus spot for overflow; benchmarking via DAT, Truckstop.com (US), MarketView, Xeneta
- Dock-scheduling automation to reduce dwell and detention
- Driver retention as a metric — driver turnover is the silent cost driver (industry runs 80–100% annual turnover at large fleets in normal years)
- For ASEAN cross-border: pre-clearance via ACTS where eligible; AEO-broker engagement to expedite; fuel and lodging cost differences across borders priced into the lane

### Failure modes
- Spot-rate dependence in tight markets — cost spikes 30–50% in capacity crunches
- Detention written off operationally rather than billed back — silent margin leakage
- ASEAN cross-border: paperwork delays at the secondary border (typically 2–6 hours each way for traditional clearance vs. <1 hour for ACTS-eligible flows)

## Rail / Intermodal

The most cost-efficient mode per ton-km after ocean, but with infrastructure dependencies.

### Service types
- **Carload** — bulk commodities (grain, coal, chemicals, automobiles)
- **Intermodal** — containers on rail
  - **COFC** (Container On Flat Car) — domestic and international; double-stack where clearances allow
  - **TOFC** (Trailer On Flat Car) — less common now
- **Unit train** — dedicated train for one commodity, point-to-point

### KPIs
- **Cycle time** (origin to destination) — door-to-door for intermodal
- **Gate transactions per hour** at intermodal ramps
- **Drayage cost** (truck portion of intermodal door-to-door)
- **Rail dwell** at terminals
- **Equipment imbalance** — empty repositioning costs

### Best practices
- For long-haul (>800 km), intermodal generally beats truckload on cost; trade-off is transit time (typically 2–3 days slower) and reliability variance
- Pre-stage at ramps — late drayage gates is a top cause of missed cuts
- Equipment-pool agreements for repositioning

### ASEAN context
- Rail freight underdeveloped vs. road in most of ASEAN
- Thai SRT ICD Lat Krabang ↔ Laem Chabang rail shuttle — operational, capacity-constrained
- Thailand-Lao railway (Nong Khai connection to China-Laos Railway) — operational since 2021; transformative for North-South freight when fully utilized
- Thai-China high-speed rail — under construction (Phase 1: Bangkok–Nakhon Ratchasima); freight implications uncertain
- Singapore–KL High Speed Rail — cancelled/revived multiple times

## Multimodal / End-to-End

When goods cross multiple modes, best practice shifts to:

- **Single contract / single liability** structures (Multimodal Transport Operator) where available — reduces coordination overhead
- **End-to-end visibility platform** (project44, FourKites, Shippeo, Wakeo) — predictive ETAs from booking through final mile
- **Common data model** across the chain — EDI 204/214/990 etc. or modern API equivalents
- **Single point of demurrage/detention accountability** — multimodal often surfaces handover-zone disputes

### Failure modes
- Mode-switch handovers losing visibility — "lost between gates"
- Bill of Lading vs. AWB vs. truck bill mismatch in legal liability
- Insurance coverage gaps at modal handovers

## Mode-selection logic

Cost ascends roughly: ocean < rail < road < air. Speed inverts. Choose by:
- **Time sensitivity** of the goods (perishables, fashion seasons, capital project schedules)
- **Value density** (USD/kg) — high-density value justifies air; low-density bulk goes ocean
- **Distance** — short-haul (<500km) air rarely makes sense; very long-haul (>10000km) ocean usually wins on cost
- **Reliability requirements** — schedule reliability varies enormously by mode and route
- **Total landed cost** — including inventory carrying cost during transit (longer mode = more pipeline inventory)

A common analytical framework: total cost = transportation cost + inventory carrying cost during transit + safety stock cost (function of lead-time variability) + cost of stockouts. Air's higher transportation cost can be more than offset by lower inventory carrying cost on high-value SKUs.
