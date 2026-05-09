# Vendor and Software Landscape

The logistics technology stack matters. Practitioners spend serious money and political capital choosing and implementing these systems. This reference is a navigable map, not an endorsement.

A note on currency: vendor positions, ownership, and capabilities shift continuously. Treat names below as a 2026 snapshot; verify current state when a procurement decision is imminent.

## The functional stack

A typical multi-system supply chain stack:

- **ERP** — financial backbone, master data, transactional spine (SAP, Oracle, Microsoft Dynamics, Workday, NetSuite for SMB)
- **OMS** — Order Management System; orchestrates orders across channels and fulfillment nodes (Manhattan Active Omni, IBM Sterling, Salesforce Order Management, Fluent Commerce)
- **WMS** — Warehouse Management System (covered separately in warehouse-operations.md)
- **TMS** — Transportation Management System; planning, execution, freight audit
- **YMS** — Yard Management System; trailer location and dock scheduling
- **Visibility platform** — real-time tracking and predictive ETAs across modes
- **Demand and Supply Planning** — forecasting and S&OP execution
- **SRM / Procurement** — supplier management and sourcing
- **Trade compliance** — classification, screening, FTA management
- **Network design / modeling** — strategic capacity and flow planning

## TMS landscape

Transportation Management Systems plan loads, tender to carriers, execute, and audit freight. Critical for shippers above ~USD 20–30M annual freight spend.

### Tier 1 (enterprise, multi-mode, multi-region)
- **Oracle OTM** (Transportation Management) — strong network optimization; common in large global manufacturers
- **SAP TM** — for SAP-integrated shops; deeper since SAP S/4HANA TM
- **Manhattan Active Transportation** — strong for retailers, integrated with Manhattan Active Omni and WMS
- **Blue Yonder Luminate Transportation** — strong analytics and network optimization
- **MercuryGate** — broad multi-mode capability; popular in 3PL space
- **e2open** — strong international and trade-compliance integration

### Tier 2 (mid-market and specialized)
- **Alpega (TMS, inet, Transwide, Wtransnet)** — European strength
- **Descartes** — broad logistics suite; strong customs and last-mile
- **Transporeon** (now part of Trimble) — strong European carrier network
- **Project44** — historically a visibility platform, expanding into adjacent execution
- **3GTMS, Cario, MyCarrierPortal, Logility, BluJay (Eyefreight)** — various mid-market positions

### Specialty / domain-specific
- **GoComet, Freightos** — international ocean rate management
- **Convoy collapsed October 2023** — important industry event; digital freight brokerage valuations contracted; consolidation continues
- **Uber Freight, Loadsmart, Flexport, Forto** — variations on digital freight brokerage and forwarding models

### Selection drivers
- Multi-mode coverage (ocean, air, road, rail, parcel)
- Geographic footprint (US-only vs global)
- Carrier network depth (especially relevant for SMB shippers)
- Integration with existing ERP/WMS
- Optimization sophistication (lane optimization, multi-stop, continuous moves)
- Visibility integration (or native visibility)
- Freight audit and payment integration
- Total cost of ownership over 5–7 years

## Visibility platform landscape

Real-time supply chain visibility platforms have matured significantly. Major players:

- **project44** — strongest in international ocean and intermodal; broad carrier integration
- **FourKites** — strong in North American truckload and retail CPG ecosystems
- **Shippeo** — European strength in road
- **Wakeo** — multi-modal European
- **OpenTrack, Loginext, TraceLink** (pharma-specific), **GroundCloud** (parcel)
- **Tive, Roambee** — sensor-based visibility (IoT trackers, cold-chain, security)

### Selection drivers
- Modal coverage matching your flow
- Carrier coverage in your relevant lanes
- Predictive ETA accuracy benchmarks (some publishers provide independent benchmarking)
- Integration depth with TMS/ERP (write-back vs read-only)
- Exception management workflow (alerting and resolution, not just dashboards)

### A senior caution
Visibility is necessary but not sufficient. A visibility platform that surfaces exceptions to nobody empowered to act on them is shelfware. The org/control-tower question (org-talent-negotiation.md) determines whether visibility creates value.

## Demand and Supply Planning vendors

The S&OP / IBP execution layer.

### Best of breed
- **o9 Solutions** — modern; strong in CPG and retail
- **Kinaxis** (RapidResponse) — strong concurrent planning; common in semiconductors and pharma
- **Anaplan** — flexibility; broad cross-functional planning use
- **OMP** — strong in process industries (chemicals, food)
- **John Galt Solutions** — mid-market

### Suite-integrated
- **Oracle Fusion / Demantra**
- **SAP IBP** (Integrated Business Planning)
- **Blue Yonder Luminate Planning**

### ML-native and newer entrants
- **ToolsGroup, Vekia, Aera Technology, Pelico** — varying degrees of ML-native architecture
- **Microsoft / OpenAI integrations** — many planning vendors layering generative and agentic AI on existing engines; capability claims should be tested rigorously, not taken at face value

## Network design and modeling tools

Strategic-decision support for network design, scenario analysis, capacity planning.

- **Coupa Supply Chain Modeler** (formerly Llamasoft Supply Chain Guru) — dominant
- **Optilogic** — newer; cloud-native
- **AnyLogic** — agent-based simulation; strong for complex what-if
- **River Logic** — prescriptive analytics
- **Excel** — still used widely for smaller-scale modeling, often inappropriately for problems that warrant proper tools

## Procurement / SRM

Sourcing, supplier management, contract management.

- **SAP Ariba** — dominant in large enterprise procurement
- **Coupa** — strong in indirect spend management; expanded into supply chain
- **JAGGAER, GEP Smart, Ivalu, Zycus, Workday Strategic Sourcing**

For supply chain risk specifically: **Riskmethods** (Sphera), **Resilinc**, **Everstream Analytics**, **Interos** — supplier risk monitoring and tier-N visibility.

## Trade compliance software

A specialty domain often under-served by general supply chain tools.

- **Descartes** — broad customs and compliance suite
- **Thomson Reuters ONESOURCE Global Trade**
- **SAP GTS** (Global Trade Services) — common in SAP shops
- **E2open** (acquired BluJay, Amber Road) — strong in FTA management and screening
- **Integration Point** (now part of Thomson Reuters)
- **SAP Watch List Screening** — sanctions screening
- **Refinitiv World-Check, Dow Jones RiskCenter, LexisNexis Bridger** — sanctions and PEP screening (cross-functional with compliance)

For Thai-specific compliance, local players (TIFFA member firms, AEO-certified brokers with technology integration) often supplement global tools.

## Last-mile and parcel

Different ecosystem from heavy freight.

- **Bringg, OneRail** — last-mile delivery management
- **Locus** — route optimization
- **Onfleet, Routific, Wise Systems** — various positions
- **Parcel rate-shopping**: ProShip, Logistyx (now part of E2open), ConnectShip, ShipHero (SMB)

In Thailand and ASEAN, the last-mile market is dominated by:
- **Kerry Express** (acquired by SF Express)
- **Flash Express** — fast-growing Thai unicorn
- **J&T Express** — Indonesian-origin, regional growth
- **Grab, Lalamove** — gig-network last-mile
- **Thailand Post (ThaiPost)** — government postal operator
- **DHL eCommerce Solutions** — international integrator's local arm

## Build vs buy

For most logistics software needs, *buy*. Custom development of TMS, WMS, planning, or compliance systems is a graveyard of ambitious failures. Configuration depth in modern systems handles ~95% of what large enterprises need.

Exceptions where build can make sense:
- **Specific competitive differentiator** — Amazon's WMS and TMS were built; their scale and uniqueness justified it. Few others share that profile
- **Integration glue and orchestration layers** — building thin integration and orchestration on top of bought systems is normal and often necessary
- **Analytics and reporting** — internal data and analytics platforms commonly built; standard products often inadequate for tailored decision support
- **Edge use cases** — specific routing constraints, niche regulations, particular customer demands sometimes warrant custom

The dominant pattern in modern enterprise: best-of-breed bought systems integrated through a modern data platform (Snowflake, Databricks, Redshift) with custom analytics and orchestration. Pure suite vendor is increasingly rare for sophisticated operators.

## Procurement playbook for logistics technology

Specific to selecting vendors:

### Pre-RFP
- **Define requirements with the people who'll use the system**, not corporate IT alone. Operators and planners must own functional requirements.
- **Reference data cleanliness** — bad data turns any implementation into a multi-year project. Cleaning data first is non-negotiable.
- **Identify integration scope clearly** — most cost overruns come from underestimated integration

### RFI / RFP / Demo
- **RFI** for capability long-list (5–10 vendors)
- **RFP** for short-list (3–5)
- **Scripted demos** with your data and your scenarios — vendor-driven demos are theater
- **Reference checks** with operators (not procurement contacts) at companies similar to yours
- **PoC** for high-stakes selections, with success criteria written before starting

### Total cost of ownership over 5 years
- License or subscription fee (cloud SaaS dominant)
- Implementation services
- Integration cost (frequently 1–3× license cost)
- Internal program management
- Ongoing operations (admin, configuration changes)
- Upgrade and reconfiguration cost
- Sunset and exit cost (often forgotten)

### Contract negotiation specifics
- **Data ownership and exit** — your data must be exportable in standard formats; written into contract
- **SLA and credits** — uptime SLAs and meaningful credit mechanisms
- **Price escalation** — annual cap (3–5% typical)
- **Termination for convenience** — at minimum at renewal points
- **Customization vs configuration** — clarity on what survives upgrades
- **Insurance and liability caps** — typical 12 months of fees; negotiate higher for material breach

## A reality check on emerging-tech claims

Vendor marketing frequently outpaces capability. As of 2026:
- **Agentic AI** — real in narrow workflows (exception classification, simple replanning, document extraction); not yet running supply chains autonomously despite the marketing
- **Digital twins** — useful for scenario planning and what-if; "always-on real-time digital twin" claims often overstate
- **Blockchain in supply chain** — mostly delivered less than promised since the 2017–2019 hype; specific use cases (high-value provenance, certain traceability mandates) are real
- **Quantum-enhanced optimization** — early; skeptical practitioner stance is appropriate
- **Generative AI for planning narrative and chart-of-the-day** — quickly maturing, useful at the analyst layer

Practitioner stance: ask vendors for live customer references doing the specific use case, not pilots. The gap between pilot success and production deployment is where most of the marketing claims dissolve.

## When this reference is most useful

- **Vendor selection underway or imminent**
- **TCO discussion with finance**
- **Architecture choice (best-of-breed vs suite, build vs buy)**
- **Vendor performance review or contract renegotiation**
- **Evaluating "AI transformation" pitches**

For shipper-and-strategy advisory work, vendor literacy makes recommendations grounded rather than abstract. Telling a CFO that "agentic AI in narrow workflows" is the right Layer 5 move is hand-waving; pointing to specific vendor categories and their actual delivery patterns is grounded advice.
