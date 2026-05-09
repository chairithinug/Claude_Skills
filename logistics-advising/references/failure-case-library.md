# Failure Case Library — Best Practices Are Written by Failures

The skill's main framework abstracts away from specific events. This reference collects canonical failures that shaped current best practice. Reach for these when illustrating *why* a recommendation matters — concrete cases land harder than principles.

Each case includes: what happened, what was lost, and what best-practice change followed.

## Pre-2010 — Foundational cases

### Boeing 787 outsourcing crisis (mid-2000s)
- **What happened**: Boeing outsourced ~70% of 787 production to global Tier-1 suppliers (Italy, Japan, Korea, US) under a "build-to-print" model expecting suppliers to integrate sub-tier components. Multiple suppliers couldn't deliver to spec on time; integration failed; Boeing absorbed billions in delays and quality remediation.
- **What was lost**: Several years of program delay, multibillion-dollar cost overruns, near-collapse of supplier relationships
- **Best practice change**: deeper visibility into Tier-2 and Tier-3 suppliers; "control points" rather than full outsourcing for critical interfaces; reshoring of selected sub-systems
- **Where it shows up**: in any tier-N visibility, supplier risk management, or core-vs-context outsourcing discussion

### Toyota Aisin Seiki fire (1997)
- **What happened**: Fire destroyed Aisin Seiki's plant producing P-valves for Toyota — a single-source critical component. Toyota's JIT system meant ~2 days of inventory across the network.
- **Recovery**: 36 of Aisin's other suppliers, plus Toyota, jointly improvised P-valve production within 5 days. Cited as proof of resilience-through-relationships rather than resilience-through-buffer.
- **Best practice insight**: relational capital with the supply base is itself a form of resilience; not all resilience is inventory or geographic diversification
- **Counter-pattern**: most organizations don't have Toyota's keiretsu relational depth; relying on this model alone is risky

## 2010–2020 — The decade that questioned globalization-and-JIT

### Tōhoku earthquake / tsunami (March 2011)
- **What happened**: 9.0-magnitude earthquake and tsunami in northeastern Japan disrupted electronics, automotive, and material supply globally. Renesas (semiconductors), various component makers offline for weeks.
- **What was lost**: Estimated USD 210B+ direct economic damage; auto industry production cuts globally for 4–6 months
- **Best practice change**: Tier-N supplier mapping (the realization that companies didn't actually know who their critical suppliers' suppliers were); the rise of supply chain risk management as a discrete function

### Thailand floods (2011, July–November)
- **What happened**: Severe flooding in Thailand inundated industrial estates in Ayutthaya and surrounding provinces — heart of global hard-disk-drive manufacturing (Western Digital, Seagate, Toshiba). HDD production capacity dropped ~30% globally.
- **What was lost**: Estimated USD 45B+ economic damage; HDD prices doubled for ~6 months; PC industry shipments dropped meaningfully
- **Best practice change**: Geographic concentration awareness; second-source manufacturing; flood-zone risk in industrial-estate selection. For Thai-based readers: the Eastern Economic Corridor (EEC) push toward Chonburi/Rayong (less flood-prone) is partly a legacy of this event.

### Volkswagen Dieselgate / supply chain ESG awareness (2015)
- **What happened**: VW's emissions cheating scandal triggered regulatory and consumer focus on supply chain integrity beyond cost and quality
- **Best practice change**: ESG due diligence in supply chain, supplier code of conduct enforcement, traceability for environmental compliance — precursors to today's CBAM, scope 3, and human-rights diligence regimes (German Supply Chain Act, EU CSDDD)

### Hanjin Shipping bankruptcy (August 2016)
- **What happened**: Hanjin, then world's seventh-largest container carrier, filed bankruptcy. Vessels arrested at ports globally; cargo stranded; ports refused to handle Hanjin ships fearing non-payment.
- **What was lost**: Estimated USD 14B in stranded cargo; weeks of disruption
- **Best practice change**: Carrier financial-health monitoring; multi-carrier strategy on critical lanes; insurance coverage review (cargo strand vs. vessel events)

## 2020–2025 — The disruption decade

### COVID-19 (2020–2022)
- **What happened**: Pandemic disrupted supply, demand, and logistics simultaneously. Container shortages, port congestion (LA/Long Beach 2021 with 100+ vessels at anchor), trucking capacity collapse, semiconductor shortage that lasted into 2023.
- **What was lost**: Hard to quantify; trillions in cumulative economic impact; lasting changes to consumer-purchasing patterns and supply-chain assumptions
- **Best practice change**: Multi-sourcing acceleration; buffer inventory restored on critical SKUs; visibility platform adoption; agentic-AI-readiness investments; nearshoring strategies. The shift from "just-in-time" to "just-in-case for the critical 20%" was largely a COVID artifact.

### Suez Canal — Ever Given grounding (March 2021)
- **What happened**: Container ship Ever Given grounded in Suez Canal, blocking traffic for 6 days. ~12% of global trade transits Suez; ~USD 9.6B/day in trade flowed through during normal operation.
- **What was lost**: ~USD 60B+ direct economic impact; weeks of ripple effects through ports
- **Best practice change**: Chokepoint awareness (Suez, Panama, Bab el-Mandeb, Hormuz, Malacca); willingness to consider longer routes (Cape of Good Hope, polar) when chokepoints disrupt; renewed attention to landbridge alternatives where geography allows

### Greensill Capital collapse (March 2021)
- **What happened**: Greensill, a major supply chain finance provider, filed insolvency. ~USD 5B+ in supply chain receivables impaired or lost; revealed opaque off-balance-sheet structures and concentration risks (notably Sanjeev Gupta's GFG Alliance).
- **What was lost**: Direct losses to investors; widespread supplier disruption among Greensill-financed programs; reputational damage to SCF as an instrument
- **Best practice change**: Accounting treatment scrutiny (FASB and IASB amended disclosure standards); clearer lines between trade payables and debt; supplier opt-in transparency in SCF programs; insurance backing transparency

### Russia-Ukraine and sanctions complexity (February 2022 onward)
- **What happened**: Most extensive Western sanctions regime since the Cold War. Energy, financial, technology, and trade sanctions on Russia. Forced wholesale review of supplier networks, vessel ownership, beneficial ownership.
- **Best practice change**: Sanctions-screening intensification; vessel-ownership and beneficial-owner screening; secondary-sanctions risk management; trade-compliance team scaling; complex routing and re-flagging detection

### Red Sea / Houthi attacks (late 2023 onward)
- **What happened**: Houthi missile and drone attacks on commercial vessels in Bab el-Mandeb forced major carriers to divert from Suez to Cape of Good Hope route. Asia-Europe transit times extended ~10–14 days; freight rates spiked.
- **What was lost**: Ongoing increased transit cost, capacity tightness in 2024, freight rate volatility
- **Best practice change**: War-risk insurance considerations; multi-mode contingency on Asia-Europe lanes; willingness to accept longer baseline transit times; geopolitical scenario planning as core practice

### Baltimore Key Bridge collapse (March 2024)
- **What happened**: Container vessel Dali struck the Francis Scott Key Bridge, collapsing the bridge and closing the Port of Baltimore for ~2.5 months. Baltimore is the largest US East Coast port for autos and a major coal export point.
- **What was lost**: ~USD 1.7B+ direct damages (insurance dispute ongoing); months of cargo diversion and extended supply chain impact
- **Best practice change**: Renewed attention to single-port concentration on US East Coast for automotive flows; insurance and liability scenarios for catastrophic events; bridge and infrastructure-strike risk awareness

### Panama Canal drought (2023–2024)
- **What happened**: Severe drought reduced Gatun Lake water levels, forcing Panama Canal Authority to reduce daily transits and impose draft restrictions. ~5% of global trade transits Panama.
- **Best practice change**: Climate-related infrastructure risk made tangible; Asia-East Coast US route alternatives reconsidered; the role of inland US transcontinental rail as a hedge

### US East Coast / Gulf Coast port strike (October 2024)
- **What happened**: ILA (International Longshoremen's Association) struck for 3 days at US East Coast and Gulf Coast ports, disrupting roughly half of US container imports. Settled with major wage agreement.
- **Best practice change**: Labor-action contingency planning; West Coast pre-positioning; reminder that the labor layer is a real risk vector independent of market or technology dynamics

## 2025–2026 — Tariff-regime restructuring

### US tariff regime restructuring (2025 onward)
- **What's happening**: Major US tariff increases beginning 2025 affecting most major trading partners; periodic adjustments and exemptions creating planning volatility
- **Practitioner reality**: Tariff classifications rechecked under audit risk; FTA preferences re-prioritized (USMCA, KORUS, Australia FTA still active); transshipment and origin scrutiny increased; DDP terms exposing exporters to open-ended tariff risk
- **Best practice change in real time**: Tariff engineering as legitimate planning discipline; HS classification audits; supplier and assembly-location reconsideration for origin optimization; Incoterm renegotiation pushing risk to the right party

### China+1 reroute saturation
- **What's happening**: Vietnam, Thailand, India, Mexico, Indonesia receiving substantial FDI redirection from China-centric manufacturing. Capacity constraints and infrastructure bottlenecks in receiving economies.
- **Practitioner reality**: Lead-time variability in Vietnam/Mexico through 2024–2025; quality variability during ramp-up; double-sourcing complexity; logistics-network reshape ongoing
- **Best practice change**: Phased relocation rather than wholesale shifts; quality and engineering investment in receiving economies; freight network redesign as a multi-year program

## How to use these cases

When recommending:
- Multi-sourcing → reference Boeing 787, COVID semiconductors
- Chokepoint awareness / route diversity → reference Ever Given, Red Sea, Panama drought
- Carrier financial-health monitoring → reference Hanjin
- Single-source reliance dangers → reference Aisin (positive; relationships saved it) and 2011 Thailand floods (negative; geographic concentration)
- SCF transparency → reference Greensill
- Sanctions and screening rigor → reference Russia-Ukraine
- Tier-N visibility → reference 2011 Tōhoku, COVID semiconductors
- Insurance and liability scenarios → reference Baltimore Key Bridge

The pattern: when a practitioner asks "is this really worth doing?", a specific case answers more persuasively than a generic principle. The cases here are not the only ones — they are the canonical ones that shaped current practice. A practitioner who knows them is recognized as one; a practitioner who doesn't gets gently dated by senior colleagues.
