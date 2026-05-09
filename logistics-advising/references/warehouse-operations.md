# Warehouse Operations — The Discipline

The skill's main body treats the warehouse as one node in the network. This reference treats it as an operating environment with its own KPIs, methods, regulatory regime, and software stack. Read whenever the question is about throughput, slotting, labor, returns, or warehouse capex.

## What a warehouse actually does

In flow order:
1. **Inbound / receiving** — ASN matching, dock scheduling, unloading, inspection, putaway
2. **Storage** — slotting (assigning SKU to location), replenishment from reserve to forward pick
3. **Order processing** — wave planning, picking (discrete, batch, zone, cluster, voice, RF, put-to-light, vision-guided)
4. **Value-added services** — labeling, kitting, repackaging, quality inspection
5. **Outbound / shipping** — packing, manifesting, loading, dispatch
6. **Returns / reverse logistics** — receiving returns, dispositioning (restock, refurbish, scrap, donate, return to vendor)

Each step has its own KPIs and best practices. A weak step bottlenecks the whole facility.

## Layout types

- **Conventional pallet rack** — selective, drive-in, push-back, pallet flow
- **High-bay AS/RS** — automated storage and retrieval; pallet shuttle and crane-based
- **Goods-to-person** — AutoStore, Exotec Skypod, Geek+, AMR-fleet picking. The "tote-to-picker" architecture has dominated new e-commerce builds since ~2018
- **Cross-dock** — minimal storage; through-flow within hours
- **Cold storage** — temperature zones (frozen <-18°C, chilled 0–4°C, controlled ambient 15–25°C); regulatory overlay for food and pharma
- **Bonded / FTZ warehouses** — under customs control (see cross-border-customs.md)

## Throughput KPIs

- **Lines per hour (LPH)** / **units per hour (UPH)** — picking rate by associate
- **Order cycle time** — receipt of order to ship-confirm
- **Dock-to-stock time** — receipt of inbound to available-to-promise
- **Pick accuracy** — typically targeting >99.5% by lines; >99.9% in pharma
- **Order accuracy** — multi-line orders, all-correct rate
- **On-time shipping** — orders shipping by promised cutoff
- **Capacity utilization** — typically aiming for 85% utilization, anything higher and you start losing efficiency to congestion

## Slotting

Where you put a SKU determines how fast you can pick it.

- **ABC velocity classification** — A SKUs (top ~20% by velocity, ~80% of picks) get golden-zone locations near pack-out; C SKUs (slow movers) get back-of-house locations
- **Affinity slotting** — SKUs ordered together placed near each other (reduces walk distance)
- **Ergonomic slotting** — heavy items at waist height; light at top/bottom; reduces injury and fatigue
- **Seasonal re-slotting** — quarterly or pre-peak; major DCs do annual deep re-slotting

A re-slot can recover 10–25% of pick productivity in a poorly-organized facility — typically the highest-ROI warehouse improvement available without capex.

## Labor management

Warehouse labor is the #1 cost line in fulfillment for most operators (50–70% of total fulfillment cost in non-automated facilities).

### Engineered labor standards (ELS)
Time-and-motion-based productivity targets per task, used by labor management systems (LMS) like Manhattan LMS, JDA/Blue Yonder, ProTrack, EasyMetrics. Properly implemented, ELS exposes underperformance and identifies process issues. Improperly implemented, ELS is a union-organizing accelerant — Amazon and others have faced sustained criticism over rate-driven injury rates.

### Direct vs contract labor
- Direct labor: lower turnover (in mature operations), better productivity, higher fixed cost
- Contract labor: faster ramp, peak flexibility, higher unit cost, more variability
- Most ops run a hybrid, ratio depending on volatility and labor market

### Retention economics
Industry turnover runs 80–150% in normal years for hourly warehouse workers. Each replacement costs 30–50% of annual wage in recruiting, training, and productivity ramp. Retention bonuses, predictable schedules, ergonomic design, and supervisor quality drive measurable retention improvements.

### Thai labor specifics
- Minimum wage adjusted by province (300–370 THB/day range as of 2024–2025; trajectory upward)
- Labor Protection Act governs hours, overtime (1.5–3× rates), holidays, severance
- Foreign worker quotas and work permits (mostly Burmese, Cambodian, Lao for warehouse roles in Thailand)
- BOI promoted operations have different labor flexibility provisions
- Social security and provident fund contributions

## Inventory accuracy

Typically 95–99% accuracy in well-run facilities; 85–95% in poorly-run; below 85% indicates systemic problems. Inventory accuracy is foundational — every downstream system depends on it.

### Sources of inaccuracy
- Miss-picks (wrong SKU, wrong quantity)
- Putaway errors (correct receipt, wrong location)
- System-physical mismatches from manual adjustments
- Theft / shrinkage
- Damaged goods not written off
- Returns not properly received

### Cycle counting vs annual physical
- **Annual physical inventory** — facility shutdown, full count; declining practice in modern WMS-driven facilities
- **Cycle counting** — daily counts of subset of locations, ABC-prioritized (A-class counted more often). Modern best practice
- **Perpetual inventory** with WMS-controlled adjustments; written-policy on tolerance bands

### Shrinkage benchmark
- Retail/distribution: typical shrink 0.5–2% of inventory value annually
- High-theft categories (small electronics, fashion): 2–5%
- Pharma, controlled substances: regulatory zero-tolerance, full reconciliation

## WMS landscape (the software question)

A WMS implementation is where many warehouse strategies die. The vendor map matters.

### Tier 1 (enterprise, complex, multi-site)
- **Manhattan Active WMS** (formerly Manhattan SCALE) — strongest for complex distribution, retail
- **Blue Yonder Luminate Warehouse Edge** — strong analytics
- **Oracle WMS Cloud** — strong for Oracle ERP shops
- **SAP EWM** — strong for SAP shops; significant complexity
- **Korber Supply Chain** — formerly HighJump; broad suite

### Tier 2 (mid-market, single or few-site)
- **Microsoft Dynamics 365 SCM** — Microsoft-stack shops
- **Softeon** — strong in 3PL multi-tenant
- **Tecsys** — healthcare, pharma strength
- **Infor WMS** (formerly GT Nexus / Lawson) — multiple variants
- **Snapfulfil** (Synergy)
- **Generix WMS** — strong in EMEA, growing in Asia

### Tier 3 (SME, basic, often pre-packaged with other tools)
- Many regional players; integration with national 3PL ecosystems
- Open-source options exist (Odoo, ERPNext) but lack depth for complex operations

### Implementation reality
- Tier 1 implementation: 9–18 months, USD 1–10M+ for a single site, longer and more for multi-site rollout
- Tier 2: 4–9 months, USD 200K–1M
- Failure rate of WMS implementations is significant — industry estimates 20–40% of major projects fail to deliver on original scope
- Common failure modes: insufficient data cleansing pre-go-live, underestimated integration complexity (with TMS, OMS, ERP), inadequate change management, vendor over-promising on fit

### Build vs buy
Almost always buy. Custom WMS development is a graveyard of projects. Configuration depth in modern WMS is sufficient for most needs.

## Returns and reverse logistics

E-commerce growth made returns a strategic concern. Return rates 10–30% in apparel; 5–15% in general merchandise; 3–8% in CPG and grocery.

### Returns flow design
- **Returns to DC** — central processing; consistent quality control; longer cycle time
- **Returns to store** (ship-from-store hybrids) — faster customer credit, harder inventory accuracy
- **Returns to dedicated returns center** — separate operation optimized for disposition decisions
- **Drop-off network** (parcel locker, drop-points) — UPS Store, USPS, Happy Returns, Asendia networks; reduces customer friction

### Disposition decisions
A returned unit has multiple paths: restock as new, restock as B-grade, refurbish, liquidate via secondary market, scrap, donate, return-to-vendor. The disposition decision drives most of the economics — restock-as-new is the only path that recovers full margin.

### Returns KPIs
- Return rate by SKU/category (signals product or sizing issues)
- Return-to-resaleable cycle time
- Recovery rate (% of original retail value recovered)
- Disposition mix
- Returns-related cost per order (separate from forward-fulfillment cost)

## OSHA and HSE

Warehouse operations carry real workplace safety obligations and personal director liability in many jurisdictions.

### Critical safety domains
- **Forklift / powered industrial truck** — OSHA 1910.178 (US); ANSI/ITSDF B56; mandatory operator training and certification, daily inspection, designated traffic patterns
- **Racking inspection** — manufacturer guidelines (RMI in US, SEMA in UK); annual structural inspection; immediate damage protocols
- **Lockout-tagout** — energy isolation during maintenance; standard procedures, training, audits
- **Fire suppression** — NFPA 13 (sprinklers), NFPA 30 (flammable liquids), high-pile storage requirements
- **Cold storage** — ammonia refrigeration safety (PHA, mechanical integrity, emergency response)
- **Manual handling and ergonomics** — back injuries are the dominant cost driver in workers' comp
- **Loading dock safety** — wheel chocks, dock locks, glad-hand procedures
- **Hazardous materials** — DOT / IMDG / IATA segregation requirements; SDS access; spill response

### Thai HSE specifics
- Ministry of Labour Notification on Occupational Safety, Health and Environment
- BOI promoted operations have specific HSE compliance requirements
- Workmen's Compensation Fund and Social Security for workplace injuries
- Annual safety audits commonly required by industrial estate operators

A facility's safety record affects insurance premiums, customer audits (especially CPG and pharma), and BOI privilege maintenance.

## Automation decision framework

Whether and how to automate a warehouse is one of the most consequential capex decisions a logistics organization makes.

### When automation pays
- High-volume, stable SKU base (low SKU velocity churn)
- Tight labor market, rising wages (Singapore, parts of Western Europe, increasingly Bangkok skilled-labor segments)
- Long-tenure facility (5+ years remaining lease)
- Predictable peak (compatible with throughput design)
- High pick accuracy requirement (pharma, electronics)

### When automation misfires
- High SKU churn / fashion / seasonal (you'll re-program constantly)
- Short-tenure facility (capex doesn't amortize)
- Variable order profile (single-line vs multi-line) — different optimal architectures
- Pre-cleanup of master data and process discipline (automating chaos = automated chaos)

### Common automation systems
- **Pallet shuttle / AS/RS** — high-density storage of full pallets
- **Goods-to-person systems** (AutoStore, Exotec, Geek+) — totes brought to picker; dominant in modern e-commerce
- **AMRs** (Locus, Fetch, 6 River, Seegrid) — collaborative robots augmenting human pickers
- **Conveyor and sorter systems** — established, deep-stack tech; still best fit for some patterns
- **Goods-to-robot picking** — vision-guided robot arms picking specific SKUs; maturing but not yet universal
- **Vision-based receiving and quality** — increasingly embedded; catches errors at the highest-leverage point

### Total cost of ownership horizon
Automation business cases must amortize capex over 7–15 years. Underestimating maintenance, software upgrades, and reconfiguration cost is the dominant business-case error. Operating models with vendor-provided uptime SLAs (RaaS — robotics as a service) are growing, shifting capex to opex.

## Warehouse-specific KPIs to add to the canonical bundle

For a shipper or retailer with significant warehouse exposure, supplement the main KPI list with:
- Lines per hour by zone and by associate
- Pick accuracy / order accuracy
- Dock-to-stock time
- Inventory accuracy (location-level and SKU-level)
- Shrinkage as % of inventory value
- Labor cost per order / per line / per unit
- Throughput at peak vs average (peak factor)
- Returns processing cycle time
- Recordable injury rate (TRIR / DART rate) — direct insurance and BOI implications

## Practitioner reality

A senior warehouse director's job is mostly about three things: **labor, layout, and software**. They will resent a "logistics framework" that doesn't speak to those concerns. The shipper-side advisory work this skill primarily supports should still place the warehouse correctly: it's where 50–70% of fulfillment cost lives, where most service-level promises succeed or fail, and where the working-capital reduction efforts of finance get delivered or destroyed.
