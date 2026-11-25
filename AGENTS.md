# AGENTS.md — DineLoop

Brief for any AI agent (or new teammate) working on DineLoop. Read this first.

## Context in six lines

1. DineLoop is the flagship CraftLayer vertical: QR table ordering + KDS + waiter app + consented diner CRM + WhatsApp marketing for Indian restaurants, cafes, bars, cloud kitchens and food courts.
2. Positioning: the **guest-revenue layer**, not a POS replacement. It sits beside Petpooja/Posist/paper at launch and earns its keep by raising AOV, bringing diners back and shifting orders off aggregators.
3. Buyer: the owner of a single independent outlet with 8–40 tables in a Tier 1–2 city. Decision in one meeting; pays from the outlet's bank account or UPI AutoPay.
4. Money model: subscription (₹999 / ₹2,499 / ₹4,999 per month, or ₹9,999 / ₹24,999 / ₹49,999 per year) + one-time setup + WhatsApp message margin + payment-partner revenue share.
5. Existing code: the founder's prototype **TableTap** ([github.com/craftLayer-studio/tabletap](https://github.com/craftLayer-studio/tabletap), Next.js + TypeScript, milestone M0, in-memory store, simulated payments) is DineLoop's ordering module: guest `/t/{table}` menu, order, live status, call waiter, GST bill, tip, even split, UPI intent link, review; `/staff` floor map; `/kitchen` station display; `/owner` day summary. Its `PLAN.md` holds the data model, order state machine and milestones M0–M3. Build DineLoop on top of it; do not restart. Coverage map: [docs/01-product-plan.md](docs/01-product-plan.md#existing-codebase-tabletap).
6. Most shared capability (QR engine, ordering, payments, CRM, WhatsApp, loyalty, games, reviews, staff app, analytics) comes from [`../core/`](https://github.com/craftLayer-studio/craftlayer-core/blob/main/README.md). DineLoop adds restaurant-specific modules: table/section model, KDS, course and modifier handling, KOT printing, GST restaurant billing, recipe costing.

## Reading order

1. [README.md](README.md) — one-page summary.
2. [docs/02-problems-and-benefits.md](docs/02-problems-and-benefits.md) — why owners buy.
3. [docs/01-product-plan.md](docs/01-product-plan.md) — what to build, in what order.
4. [docs/05-pricing-and-revenue.md](docs/05-pricing-and-revenue.md) — what to charge, unit economics.
5. [docs/06-go-to-market-and-onboarding.md](docs/06-go-to-market-and-onboarding.md) — how to sell and onboard.
6. [docs/04-market-research.md](docs/04-market-research.md) — evidence and sources.
7. [docs/03-pros-cons-risks.md](docs/03-pros-cons-risks.md) — risks and kill criteria.

## Glossary

| Term | Meaning |
|---|---|
| QR ordering / scan-and-order | Diner scans a table QR, opens a web menu (no app), places an order tied to that table |
| KDS | Kitchen display system: screen/tablet in the kitchen showing live orders by station |
| KOT | Kitchen order ticket, the printed slip many Indian kitchens still use |
| Captain / captain app | Indian term for the head waiter and the waiter ordering app |
| Aggregator | Zomato, Swiggy (and ONDC buyer apps) that list restaurants and charge commission |
| Direct ordering | Restaurant's own ordering link/site; no marketplace commission |
| AOV | Average order value per bill |
| Table turnover | Number of seatings per table per service |
| Opt-in | Explicit, recorded consent from a diner to receive WhatsApp marketing (DPDP + Meta policy) |
| Data Principal / Data Fiduciary | DPDP Act terms: the diner / the restaurant (DineLoop is the Data Processor) |
| WABA | WhatsApp Business Account via the Cloud API |
| Utility vs marketing message | Meta template categories; utility (bill, order status) is far cheaper than marketing |
| ARPU | Average revenue per paying outlet per month |
| Win-back | Campaign to diners who have not visited in N days |

## Decisions made

| # | Decision | Reason |
|---|---|---|
| D1 | Web-based diner flow (PWA), no diner app download | Download kills conversion at the table; all serious QR players work this way |
| D2 | Integrate with existing POS before replacing it | Owners already paid Petpooja for the year; replacement is a slow, risky sale |
| D3 | Ship a light GST billing module in Growth | ~Half of small cafes still bill on paper or Excel (estimate); gives a POS-lite path |
| D4 | No commission on dine-in or direct orders | Our whole pitch is "escape commission"; revenue comes from subscription |
| D5 | Phone capture by OTP with DPDP notice, never forced to view menu | Forced capture angers diners and breaks consent rules; offer value (bill on WhatsApp, game, points) instead |
| D6 | WhatsApp billed at cost plus margin, credits prepaid | Meta rates change (marketing rose to ~₹0.86 in 2026); prepaid avoids bad debt |
| D7 | Founder-led field sales in one city cluster first | Restaurant owners buy on trust and demos, not ads |
| D8 | Product name DineLoop kept for the suite | No established brand found in restaurant software; "TableTap" is crowded (see open questions) |
| D9 | TableTap codebase is the ordering/KDS/pay module of DineLoop | M0 already covers ~60% of the P0 ordering flow with tested domain logic; rewriting wastes 3–4 weeks |
| D10 | Follow TableTap PLAN.md for data model, state machine, multi-tenancy (RLS), SSE and payment rules | Sound design; extend it with CRM, consent and campaign tables rather than fork it |

## Open questions

1. **Name check.** Searches on 2026-11-24 found no established restaurant-software brand called "DineLoop". Unrelated "Dine" apps exist. Before launch: check trademark class 9/42 on the IP India public search, the dineloop.com / dineloop.in domains and Play Store. Backup names if blocked: **TableLoop**, **ServeLoop**.
2. **Should the whole suite be branded TableTap instead of DineLoop?** Recommendation: **no. Keep DineLoop as the product and company-facing brand; keep "TableTap" as the internal codename of the ordering module (or rename the repo later).** Reasons:
   - Name conflicts. A search on 2026-11-24 found at least four "TableTap" restaurant-tech uses: Table Tap LLC, a US self-pour/tableside ordering company with its TableTender product ([Loyalty360](https://loyalty360.org/content-gallery/daily-news/table-tap-brings-customer-engagement-to-next-level-with-launch-of-tabletend)); a "TableTap" AI restaurant SaaS with QR ordering, KDS and POS on Product Hunt ([producthunt.com/products/tabletap-2](https://www.producthunt.com/products/tabletap-2)); a "TableTap - Restaurant" iPad management app ([App Store](https://apps.apple.com/us/app/-/id6747565023)); and a QR ordering web demo ([tabletapuq.onrender.com](https://tabletapuq.onrender.com/tabletap/)). That makes trademark, domain, SEO and app-store search hard, and blocks a global launch.
   - Scope. "TableTap" describes the at-table moment only. The money in DineLoop is the loop after the meal: CRM, WhatsApp win-back, loyalty, reviews, direct ordering. Cloud kitchens and delivery have no table.
   - Portfolio fit. CraftLayer names describe the business outcome (RepVault, StayBell). "Loop" signals repeat customers, which is the core pitch.
   - Cost of switching later is low: no customers and nothing deployed yet.
   - Counter-argument: "TableTap" is easier to say and demo, and the repo already uses it. Mitigation: use "Tap to order" as a feature label inside DineLoop ("DineLoop Tap").
3. Which POS integration first: Petpooja (largest base, 100,000+ restaurants per [Entrackr](https://entrackr.com/news/petpooja-raises-155-mn-series-c-at-over-3x-valuation-premium-10512396)) or Posist? Petpooja has a partner API program; confirm terms.
4. Payment partner: Razorpay (2% standard platform fee on UPI) vs Cashfree/PhonePe PG with negotiated UPI rate. Need a split-settlement rate under 1% for UPI to keep diner payments attractive.
5. Do bars need age-gated menus or state excise rules for displaying liquor prices online? Check per state before selling to bars.
6. Will Meta's charge on service messages from 1 October 2026 change the cost of order-status updates? Recheck the rate card each quarter.
7. Is a self-serve sign-up flow worth building before 100 customers, or stay sales-led?
8. Hardware bundle: sell Android KDS tablets and thermal printers at cost, or partner with a distributor?

## Rules for agents editing these docs

- Follow [../CONVENTIONS.md](https://github.com/craftLayer-studio/craftlayer-products/blob/main/CONVENTIONS.md). Cite every number with URL + access date, or mark **(estimate)** with reasoning.
- Do not re-spec core modules; link to `../core/`.
- Every feature row must name the metric it moves.
- Any change touching diner phone numbers must keep DPDP notice, opt-in, opt-out and purpose limitation intact.
