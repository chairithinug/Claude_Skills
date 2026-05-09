# Compliance Beyond Clearance — Audit, Sanctions, Export Controls

The customs reference covers *clearance* — pre-arrival and at-the-border. This reference covers what happens *after* clearance and *outside* clearance: post-clearance audit risk, denied-parties screening, export classification, recordkeeping discipline. Most of the real penalty exposure lives here, not in the clearance step.

## The post-clearance audit lifecycle

Customs administrations across APEC operate risk-based audit programs. Audits typically reach back 3–7 years depending on jurisdiction. A practitioner's exposure is determined less by what cleared the border and more by what the audit trail shows years later.

### Typical post-clearance audit triggers
- HS classification anomalies vs. peer importers
- Valuation declarations inconsistent with public pricing or related-party transfer prices
- FTA preference claims with weak origin documentation
- Repeated low-value declarations vs. similar goods peers
- Random selection (every administration runs a baseline)
- Whistleblower reports (US has CBP and DOJ False Claims Act bounties; EU has whistleblower directives)

### What auditors actually request
- Original commercial invoices, contracts, payment evidence
- Manufacturer's affidavits and Bills of Materials supporting origin claims
- Production records and process documentation for substantial-transformation claims
- Royalty agreements, license agreements, commission contracts (for valuation additions)
- Related-party transfer pricing studies
- Internal classification rulings, advance rulings sought
- Three to seven years of records depending on regime

### Recordkeeping requirements (jurisdiction-dependent — verify locally)
- **United States**: 5 years from date of entry under 19 CFR 163
- **European Union**: 3 years post-customs declaration under Union Customs Code, longer for some FTA records
- **Thailand**: 5 years under Customs Act B.E. 2560 (2017), Section 116
- **Japan**: 7 years for major records
- **China**: 3 years for general records, longer for special programs

Records must be retrievable, legible, and tied to specific declarations. Electronic recordkeeping is acceptable in most regimes provided integrity controls exist.

## Penalty regimes — why this gets resourced

### Thailand (Customs Act B.E. 2560)
- **Section 27** — false declaration: penalty up to 4× duty + VAT shortfall, goods may be seized, criminal exposure including imprisonment
- **Section 99** — smuggling: 4× duty + value of goods, seizure, criminal exposure
- **Section 202** — failure to maintain records: administrative penalty
- Personal criminal exposure for company directors in serious cases — *this is the reason Thai compliance budgets exist*

### United States (19 USC 1592)
- Negligence: up to 2× lawful duty (or 20% of dutiable value if duty-free)
- Gross negligence: up to 4× lawful duty (or 40% of dutiable value)
- Fraud: up to domestic value of merchandise — can far exceed the duty itself
- Plus separate civil penalty schedules under FTA-specific provisions and special programs (e.g., AD/CVD evasion under EAPA)

### European Union (Union Customs Code, Member State implementing law)
- Penalties harmonized in principle, set by Member State in practice
- Range from administrative fines to criminal sanctions for serious cases
- AEO status revocation as a parallel administrative consequence

### Common pattern across regimes
Penalties scale with culpability: simple errors → administrative correction; negligence → multipliers on duty; fraud → multiples of merchandise value plus criminal exposure. The audit determines which bucket you sit in — and the documentation determines what the auditor concludes.

## Voluntary self-disclosure / Prior disclosure

When you discover your own compliance error, a properly-filed prior disclosure dramatically reduces penalty exposure.

- **US**: Prior Disclosure under 19 CFR 162.74 — caps penalty at interest only for negligence, eliminates fraud penalty multiplier provided disclosure is timely and complete (before audit notification)
- **EU**: Self-disclosure provisions under Member State law; AEO status often supports favorable treatment
- **Thailand**: Self-disclosure framework less codified than US/EU; informal practice exists, but legal protection is weaker — engage a licensed Thai customs broker and counsel early

Best practice: any compliance review that surfaces material errors triggers a self-disclosure decision in 30 days or less. Sitting on a known error is the worst position; the protection lapses once the customs administration identifies the issue.

## Sanctions and denied-parties screening

Cross-border trade carries sanctions exposure regardless of customs clearance status. Sanctions are separate from duty; they prohibit transactions outright with designated persons, entities, vessels, aircraft.

### Major sanctions lists practitioners screen against
- **US OFAC SDN** (Specially Designated Nationals) — extraterritorial reach via USD clearing
- **US OFAC Sectoral Sanctions** (SSI) — limited prohibitions on specific sectors
- **US BIS Entity List** — export licensing restrictions for specified entities
- **EU Consolidated Sanctions List**
- **UK OFSI Consolidated List**
- **UN Security Council Sanctions List**
- **Country-specific lists** — Australian, Canadian, Japanese, Singaporean, Korean equivalents

### Practitioner workflow
- **Real-time screening** at customer onboarding, supplier onboarding, before each transaction
- **Ongoing screening** — lists update frequently; today's clean party is tomorrow's designated party
- **Vessel and beneficial-ownership screening** — particularly for ocean shipments; vessel sanctions designations have proliferated since Russia-Ukraine
- **Documentary trail** — proof of screening at the time of transaction is the audit defense

Software vendors: Refinitiv World-Check, Dow Jones RiskCenter, LexisNexis Bridger, Sayari, Kharon. Some ERP/TMS systems integrate screening; many don't.

### Sanctions enforcement risk reality
- US extraterritorial enforcement reaches non-US parties via secondary sanctions and USD-clearing exposure
- BNP Paribas paid USD 8.9B in 2014 for sanctions violations; Standard Chartered paid USD 1.1B in 2019
- For Thai/ASEAN exporters dealing with sanctioned counterparties — even unintentionally — the risk is real and growing

## Export controls

Distinct from sanctions and from import customs. Export controls regulate *what* can be exported, *to whom*, *for what end use*.

### Major regimes
- **US EAR** (Export Administration Regulations) — administered by BIS; covers dual-use items; ECCN classification system; Commerce Country Chart determines license requirements
- **US ITAR** (International Traffic in Arms Regulations) — administered by DDTC; covers defense articles per the USML (US Munitions List); much stricter than EAR
- **EU Dual-Use Regulation** (2021/821) — Annex I list of controlled dual-use items; member-state issuing authorities
- **Wassenaar Arrangement** — multilateral; 42 participating states coordinate dual-use and conventional arms export controls
- **Australia Group** — chemical/biological weapons-related dual-use
- **Missile Technology Control Regime (MTCR)**
- **Nuclear Suppliers Group (NSG)**

### What gets controlled
- Telecommunications and information security products (encryption above certain thresholds)
- Semiconductors (especially advanced nodes — heavily controlled since 2022 US restrictions on China)
- Toxic chemicals and precursors
- Materials for high-performance applications (composites, specific alloys)
- Aerospace components, propulsion, navigation
- Surveillance and biometric technologies (newer additions)

### "Deemed export" rules
US EAR treats disclosure of controlled technology to a foreign national *inside the US* as an export to that person's country. Practical implication: hiring decisions, lab access, software access are export-control issues. ASEAN-based subsidiaries of US firms encounter this when receiving technical data or hosting US visitors.

### End-Use / End-User verification
- US "Know Your Customer" guidance (BIS Red Flags) — screening obligations beyond entity list
- Diversion risk management — exports may not be re-exported to prohibited destinations
- Actual deliveries to designated end-users (military, WMD-related, certain governments) prohibited even if entity not listed

### Practitioner action
For Bangkok-based practitioners doing electronics, semiconductors, AI/ML hardware or software, surveillance, aerospace, or advanced materials — export controls are a first-class concern. Best practice:
- Classify products against controlled lists (ECCN for US-origin items, EU dual-use Annex I codes, etc.)
- Screen end-users for prohibited categories
- Document end-use statements in commercial agreements
- Maintain license records and authorization to support reexport claims
- Engage trade compliance counsel for ambiguous cases — penalties are severe (US EAR violations: up to USD 350K or 2× value per violation, plus criminal exposure)

## Anti-Bribery and Corruption (FCPA / UK Bribery Act / Thai NACC Act)

A specific risk in cross-border logistics: facilitation payments at land borders, ports, and customs offices. Treated differently across regimes:

- **US FCPA** — facilitation payments narrowly permitted but corporate compliance programs typically prohibit
- **UK Bribery Act 2010** — facilitation payments are bribery; no carve-out
- **Thailand NACC Act (B.E. 2542 / 1999, amended 2015 and 2018)** — strict; corporate liability for failure to prevent bribery introduced 2018
- **OECD Anti-Bribery Convention** — most APEC members signatories, with implementation varying

Practitioner reality: certain corridors and crossings have informal-payment cultures. A compliant operator must:
- Train field operators on what is and isn't permissible
- Provide alternatives (legitimate expediting fees with receipts where they exist, AEO programs, customs broker engagement)
- Document anomalies — refused payment requests, observed delays, alternate-route choices
- Implement third-party due diligence on customs brokers and agents (they are the high-risk vector)

This intersects with sanctions and export controls in trade compliance programs because the underlying compliance infrastructure (screening, recordkeeping, training) is shared.

## CBAM and emerging carbon-border regimes

EU Carbon Border Adjustment Mechanism (CBAM) — transitional reporting period 2023–2025; full operational phase from 1 January 2026. Importers of cement, electricity, fertilizer, iron and steel, aluminum, hydrogen must report embedded emissions and surrender CBAM certificates from 2026.

For ASEAN exporters: even if not directly CBAM-liable, your EU customers will demand emissions data on covered goods. UK CBAM proposed for 2027 (consultation completed). Other regimes (Japan, Australia, Canada, Korea) under various stages of consideration.

This is becoming a **trade compliance** function alongside customs and sanctions, not a sustainability function.

## Practitioner action checklist

For a cross-border practitioner, baseline compliance hygiene:

1. **Classification governance** — current HS codes by SKU, advance rulings for ambiguous goods, classification audit annually
2. **Valuation governance** — transfer pricing alignment for related-party imports, royalty/commission/assist treatment documented, arm's-length evidence retained
3. **Origin and FTA discipline** — cumulation calculations documented, manufacturer affidavits current, certificate-of-origin issuance audit trail
4. **Records retention** — 5–7 years minimum, retrievable by entry, integrated with ERP
5. **Sanctions screening** — at onboarding and per-transaction, dated audit log, vessel and beneficial-owner coverage
6. **Export classification** — ECCN/dual-use lookup at SKU master, license records where applicable, end-user/end-use due diligence
7. **AEO/trusted-trader status** — pursued where volumes justify; supports both clearance speed and post-clearance audit defense
8. **Self-disclosure protocol** — written internal policy on error discovery, escalation path, 30-day decision rule
9. **Training cadence** — annual refresh for operators, role-specific deep training for declarants, brokers, traders
10. **External counsel relationship** — pre-established for sanctions, export control, and customs penalty matters; you do not want to be looking for counsel in the 24 hours after a CBP detention notice

The cost of running these programs is non-trivial. The cost of not running them is unbounded.
