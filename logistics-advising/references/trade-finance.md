# Trade Finance & Freight Economics — Layer 4 Detail

The financial instruments and rate components practitioners actually transact in. Read whenever a finance lever is on the table or a rate-component question comes up.

## Payment instruments along the trust spectrum

Ordered from most-secure-for-seller to most-secure-for-buyer:

### 1. Cash in advance (most secure for seller)
Buyer pays before shipment. Seller has zero risk; buyer carries everything.
- *Used when*: new relationship, weak buyer credit, high political risk, custom-made high-value goods
- *Cost*: opportunity cost on buyer's working capital; reputational signal of seller's risk aversion

### 2. Letter of Credit (LC)
Bank-intermediated payment guarantee. Buyer's bank (issuing bank) commits to pay seller against compliant document presentation. Governed by **UCP 600** (ICC).

Variants:
- **Sight LC** — payment on presentation of compliant documents
- **Usance / Term LC** — deferred payment (e.g., 60/90/120 days after sight)
- **Standby LC** (SBLC) — default-triggered guarantee; effectively bank-guaranteed performance bond
- **Back-to-back LC** — intermediary trade; primary LC backs a secondary LC to actual supplier
- **Transferable LC** — partially or wholly transferable to other beneficiaries (commodity trading)
- **Confirmed LC** — second bank (typically in seller's country) adds its own guarantee, removing issuing-bank country risk
- **Revolving LC** — automatically reinstates for repeated shipments

Practitioner traps:
- **Strict compliance** — banks examine documents for letter-perfect compliance with LC terms; any discrepancy can trigger rejection. ~70% of first presentations have at least one discrepancy industry-wide.
- **Fraud risk** — UCP 600 is documentary; banks pay against documents, not actual goods. Documentary fraud bypasses the system.
- **Cost** — 0.1–1.0% of LC value per quarter typical for issuance/confirmation; expensive vs. open account
- **Working-capital lock-up** — issuing bank typically requires margin or facility against the LC

### 3. Documentary collections (D/P, D/A)
Cheaper than LC, weaker security. Banks act as agents handling documents but do not guarantee payment. Governed by **URC 522** (ICC).

- **D/P (Documents against Payment)** — buyer's bank releases shipping documents only against payment. Title transfers when buyer pays.
- **D/A (Documents against Acceptance)** — buyer's bank releases documents against buyer's acceptance of a time draft (promise to pay at maturity). Buyer gets goods on credit; risk of non-payment at maturity sits with seller.

Used in established relationships where LC is overkill but open account is too risky. Common in commodity trade.

### 4. Open account
Goods shipped before payment; payment on agreed terms (Net 30/60/90+). Dominant in mature buyer-seller relationships, intra-group trade, and developed-market B2B.

- *Pro*: lowest transaction cost, fastest cycle
- *Con*: full counterparty risk on seller; usually requires trade credit insurance to manage

### 5. Consignment / cash against documents
Variants where seller retains title or risk longer.

## Supply Chain Finance (SCF) / Reverse Factoring

Buyer-led program where suppliers can discount approved invoices early, financed at the buyer's (typically better) cost of funds.

- *Buyer benefit*: extended payment terms without harming supplier liquidity
- *Supplier benefit*: faster payment at near-buyer's funding cost
- *Bank/platform benefit*: low-risk receivables financing

**Greensill Capital collapse (March 2021)** is the case study: opaque off-balance-sheet structures, inadequate insurance backing, concentration risk. The episode reshaped accounting and disclosure expectations for SCF programs (FASB and IASB issued amended disclosure standards).

Best practice: clear accounting treatment (trade payable vs. debt classification), disclosure of program terms, supplier opt-in not opt-out, insurance backing transparency.

## Other trade finance instruments
- **Pre-shipment finance** — working capital to fund production for confirmed orders
- **Post-shipment finance** — bridges seller's cash gap between shipment and buyer payment
- **Invoice factoring** — sale of receivables to factor at discount; recourse or non-recourse
- **Forfaiting** — medium-term receivables purchase (typically capital goods, 6 months to 7 years), without recourse, fixed rate
- **Bill discounting** — discounting of accepted bills of exchange for early payment

## Trade credit insurance

Covers seller against non-payment by buyers (commercial and political risk). Major underwriters: Coface, Atradius, Allianz Trade (formerly Euler Hermes), Sinosure (China-government-backed for Chinese exporters), EXIM banks of various countries.

- Premium: typically 0.1–0.5% of insured turnover
- Coverage: typically 80–95% of invoiced value
- Often a precondition for non-recourse factoring
- Useful proxy: when a credit insurer pulls coverage on a buyer, that's a signal worth heeding

## Freight rate components — auditable line items

Best practice: never sign a freight contract without explicit definitions of every adjustable component. Common ocean freight rate stack:

- **Base ocean rate** (per TEU/FEU/CBM/RT)
- **BAF / Bunker Adjustment Factor** — fuel cost surcharge; formula-driven
- **CAF / Currency Adjustment Factor** — FX surcharge for currency mismatches
- **THC / Terminal Handling Charge** — at origin and destination, distinct
- **ISPS / Security surcharge** — post-9/11 port security cost
- **Peak Season Surcharge (PSS)** — typically Q3 transpacific, holiday-driven
- **GRI / General Rate Increase** — periodic carrier-driven increases (transpacific common)
- **ENS** (EU pre-arrival), **AMS** (US pre-arrival), **AFR** (Japan), **ACI** (Canada) — pre-arrival manifest filing fees
- **Low-Sulfur Fuel Surcharge** — post-IMO 2020 regulation requiring 0.5% sulfur fuel
- **Equipment imbalance surcharge** — empty repositioning cost recovery
- **War Risk surcharge** — Red Sea diversions since late 2023 added meaningful cost on Asia-Europe lanes

Best practice: contract defines BAF formula (or fixed-rate clauses), THC quantum, PSS notification period, and any other surcharge mechanics. Spot bookings often surprise with surcharges contract bookings would exclude.

## Demurrage & detention — distinct concepts often conflated

- **Demurrage** — container at port/terminal beyond free time (typically 4–7 days at LCB)
- **Detention** — container outside terminal, with consignee or in transit, beyond free time (typically 5–10 days at LCB)
- **Per-diem** — daily charge after free time, escalating in tiers (e.g., $50/day days 1–7, $100/day days 8–14, $200/day day 15+)
- **Combined demurrage and detention** at some carriers; understand which definition applies

Best practice:
- Track as distinct KPI with $/year exposure
- Root-cause split: carrier-caused (vessel late, equipment unavailable), customs-caused (inspection holds), consignee-caused (slow pickup, document delays)
- Negotiate free-time terms in contract — carriers will extend when volume justifies
- Visibility platform integration to flag at-risk shipments before they hit per-diem

## Insurance — cargo coverage

Institute Cargo Clauses (ICC) under Incoterms 2020:
- **ICC (A)** — all-risks cover; the broadest standard
- **ICC (B)** — named perils, intermediate cover
- **ICC (C)** — named perils, narrowest cover; minimum required under Incoterms CIF

War risk and strikes (SRCC) typically separate clauses or extensions.

Practitioner best practice:
- Don't accept ICC (C) as default — it excludes many real risks (theft, water damage in non-named circumstances, etc.)
- For high-value or sensitive cargo, all-risks ICC (A) plus war/SRCC extensions
- Self-insurance (open cover policies, captive insurance) economically attractive for high-volume shippers
- Marine claims process: notice of loss within survey period, documented chain of custody, condition surveys at handover points

## Finance KPIs worth tracking
- **Cash-to-Cash cycle time** (DIO + DSO − DPO) — top-quartile <30 days
- **Days Payable Outstanding** for SCF program participants — extension achieved without supplier liquidity damage
- **LC discrepancy rate** — % of first presentations that fail on document compliance
- **Demurrage & detention exposure** ($/year, per lane, per root cause)
- **Freight audit recovery rate** — typically 1–3% of audited spend
- **Trade credit insurance loss ratio** — claims / premium; signals portfolio health
- **FTA preference utilization** — % of eligible flows actually claimed

## Where these finance levers compound

The under-appreciated insight: **Layer 3 (cross-border) and Layer 4 (finance) compound**. Example:
- Switching from MFN to ATIGA preference saves duty (Layer 3)
- The freed cash improves DPO (Layer 4)
- Better DPO improves Cash-to-Cash (Layer 4)
- Better C2C raises ROA which improves credit terms with banks (Layer 4)
- Better credit terms enable longer LC tenors or larger SCF programs (Layer 4)

Most "logistics" decks pitch Layer 4 individually. The compounding view is the persuasive one.
