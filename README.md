# DineLoop

**Tagline:** Every table becomes a till, a waiter and a marketing channel.

DineLoop is the CraftLayer flagship for restaurants, cafes, bars, cloud kitchens and food courts. A QR code on each table lets diners browse, order, play and pay from their phone. Orders land instantly on a kitchen display (KDS) and the waiter app. Every scan can become a consented diner profile, which the owner uses for WhatsApp re-marketing, loyalty, birthday offers, Google reviews and commission-free direct ordering.

It is not "another POS". It is the **guest-revenue layer**: the part of the stack that brings diners back and moves orders off Zomato/Swiggy. It runs alongside the outlet's existing POS (Petpooja, Posist/Restroworks, or paper) from day one, and adds its own GST billing for outlets that have none.

**Existing code:** the ordering, KDS and pay module already exists as the TableTap prototype ([github.com/craftLayer-studio/tabletap](https://github.com/craftLayer-studio/tabletap), milestone M0, in-memory, simulated payments). What it covers and what DineLoop still needs: [docs/01-product-plan.md](docs/01-product-plan.md#existing-codebase-tabletap).

## Who it is for (ICP)

| Segment | Fit | Why |
|---|---|---|
| Independent cafes and casual-dining restaurants, 8–40 tables, Tier 1–2 cities | Primary | Waiter shortage, high repeat potential, owner makes the decision alone |
| Bars, pubs, microbreweries | Primary | High ticket size, repeat-driven, upsell-heavy menus |
| QSR / food courts with token counters | Secondary | Self-ordering cuts queue time; token display |
| Cloud kitchens | Secondary | Want direct ordering to escape aggregator commission; no tables |
| Chains of 3–20 outlets | Expansion | Multi-outlet reporting, central menu, CRM across outlets |

## Top features (P0 = in the 6–8 week MVP)

| Priority | Feature | Metric it moves |
|---|---|---|
| P0 | Table QR menu, order and UPI pay (no app download) | Revenue (AOV), activation |
| P0 | Kitchen display + waiter app with live order status | Retention (fewer errors), table turnover |
| P0 | Consented diner capture (OTP + DPDP notice) into CRM | Retention, referral |
| P0 | Google review funnel after payment | Acquisition |
| P0 | WhatsApp campaigns: win-back, birthday, offers | Retention, revenue |
| P1 | Wait-time mini-games that award coupons | Retention, data capture rate |
| P1 | Direct online ordering site with 0% commission | Revenue (margin), retention |
| P1 | Smart upsell prompts and combos | Revenue (AOV) |
| P1 | Loyalty points and visit-based stamps | Retention |
| P2 | Inventory, recipe costing and wastage | ARPU (Pro upsell) |
| P2 | Multi-outlet dashboard and staff attendance | ARPU, expansion |

Full list with rationale: [docs/01-product-plan.md](docs/01-product-plan.md).

## Pricing summary

| Plan | INR / month (billed yearly) | USD equivalent | For |
|---|---|---|---|
| Starter | ₹999 (₹9,999/yr) | ~$11 | QR ordering + KDS + waiter app + basic CRM, 1 outlet |
| Growth (recommended) | ₹2,499 (₹24,999/yr) | ~$28 | + WhatsApp marketing, games, loyalty, review funnel, direct ordering, GST billing |
| Pro | ₹4,999 (₹49,999/yr) per outlet | ~$57 | + inventory/recipe costing, multi-outlet, POS/aggregator integrations, staff |

One-time setup with printed QR standees: ₹4,999 (waived on annual Growth). WhatsApp messages billed at Meta cost plus a margin. Anchored below Petpooja's published ₹20,000–30,000/yr bundles ([petpooja.com/pricing](https://petpooja.com/pricing), accessed 2026-11-24). Details: [docs/05-pricing-and-revenue.md](docs/05-pricing-and-revenue.md).

## Documents

| File | What is inside |
|---|---|
| [AGENTS.md](AGENTS.md) | Context, glossary, decisions, open questions for AI agents |
| [docs/01-product-plan.md](docs/01-product-plan.md) | Vision, personas, journeys, P0/P1/P2 features, data model, integrations, metrics |
| [docs/02-problems-and-benefits.md](docs/02-problems-and-benefits.md) | Problem, solution and benefit per stakeholder |
| [docs/03-pros-cons-risks.md](docs/03-pros-cons-risks.md) | Pros, cons, risks with mitigations, kill criteria |
| [docs/04-market-research.md](docs/04-market-research.md) | Market size, competitors, pricing benchmarks, trends, regulation, sources |
| [docs/05-pricing-and-revenue.md](docs/05-pricing-and-revenue.md) | Tiers, add-ons, revenue streams, unit economics, 12-month scenarios |
| [docs/06-go-to-market-and-onboarding.md](docs/06-go-to-market-and-onboarding.md) | First 10 customers, sales script, objections, onboarding checklist, retention |

Shared platform modules: [../core/README.md](https://github.com/craftLayer-studio/craftlayer-core/blob/main/README.md).

## Licence

Source-available under the [PolyForm Noncommercial License 1.0.0](LICENSE.md). Personal, educational, research and non-profit use is free. **Any commercial use requires a paid licence or written permission from CraftLayer Studio.** See [COMMERCIAL-LICENSE.md](COMMERCIAL-LICENSE.md).

Part of the [CraftLayer Products](https://github.com/craftLayer-studio/craftlayer-products) portfolio.
