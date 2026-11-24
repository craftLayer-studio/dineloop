# 03 — Pros, cons, risks and kill criteria

## Pros

| Pro | Why it matters |
|---|---|
| Huge, growing market | Indian food services ₹5.69 lakh crore in FY24, projected ₹7.76 lakh crore by FY28; organised share grows faster at 13.2% CAGR ([NRAI IFSR 2024 via Restaurant India](https://www.restaurantindia.in/article/india-to-be-the-3rd-largest-food-service-market-by-2028-overtaking-japan-nrai-ifsr-2024)) |
| Hot owner pain | Aggregator commission fights are front-page news (restaurant boycotts in 2025 and Bengaluru boycott threat in 2026, see 04) |
| Code already exists | TableTap M0 gives tested domain logic for menu, cart, order state machine, bill split and UPI links; 3–4 weeks saved (estimate) |
| Shared core | CRM, WhatsApp, loyalty, games, reviews are built once in `core/` and reused by 10 other CraftLayer products |
| Clear ROI story | One extra table a week pays for Growth; owners can see campaign revenue in the dashboard |
| Low marginal cost | Web app, no hardware required, WhatsApp billed at cost plus margin |
| Proven elsewhere | QR ordering and pay-at-table scaled in Australia/UK (Mr Yum + me&u merger, 2023) and Owner.com raised ~$419M on direct ordering in the US ([Sacra](https://sacra.com/c/owner)) |

## Cons

| Con | Impact |
|---|---|
| Crowded market | Petpooja (100,000+ restaurants), Posist/Restroworks, DotPe, UrbanPiper, Thrive, plus dozens of cheap QR menu tools |
| Price-sensitive buyers | Small cafes compare against free QR menus and ₹5,000/yr billing tools |
| POS incumbency | Most target outlets already paid for a POS for the year; we must coexist first |
| Field sales needed | Restaurant owners buy after a demo in their outlet; slow and city-bound |
| Diner behaviour varies | Families and older diners in Tier 2–3 still prefer a waiter; QR adoption will not hit 100% |
| WhatsApp cost drift | Meta raised India marketing rates ~10% in 2026 and started charging service messages from 1 October 2026 ([MyOperator](https://myoperator.com/blog/whatsapp-business-api-pricing-india-2026)) |
| High SMB churn | Restaurants close often; churn is structural in this segment |

## Risks and mitigations

| # | Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|---|
| R1 | Petpooja bundles QR + CRM cheaper and owners stay put | High | High | Coexist via integration; sell "guest growth" outcomes (reviews, repeat visits) not features; undercut on Starter; better WhatsApp/games UX |
| R2 | Low phone-capture rate (diners refuse OTP) | Medium | High | Value exchange: bill on WhatsApp, game prize, loyalty points; never block the menu; measure capture per table and A/B the copy |
| R3 | DPDP non-compliance (consent, notice, erasure) | Medium | Very high (penalties up to ₹250 crore under the Act) | Consent ledger from day one, separate marketing tick, STOP handling, data-erasure flow, DPA with each restaurant (we are processor), follow DPDP Rules 2025 phase-in (core obligations by May 2027) |
| R4 | WhatsApp number bans for spam | Medium | High | Only opted-in contacts, frequency cap (max 4 marketing messages per diner per month), quality-rating monitor, approved templates |
| R5 | Aggregators retaliate (ranking penalties for outlets pushing direct ordering) | Low–medium | Medium | Do not touch aggregator packaging; promote direct ordering to *existing* dine-in diners only |
| R6 | Payment gateway fees make UPI in-app look worse than a soundbox | Medium | Medium | Negotiate UPI at under 1% or keep UPI intent + staff confirm option; gateway only for cards and split |
| R7 | Kitchen staff ignore the KDS in a rush | Medium | Medium | KOT printer fallback (P1), sound alerts, big type; train the chef on day 1 |
| R8 | Founder bandwidth: 11 products in portfolio | High | High | DineLoop is flagship; other products reuse core; do not start a second vertical until DineLoop has 30 paying outlets |
| R9 | Outlet closures cause churn | High | Medium | Annual prepay, focus on outlets older than 12 months, multi-outlet brands |
| R10 | Prank or fake QR orders | Low | Low | Staff confirm before kitchen (already in TableTap), rotating table tokens, rate limits |
| R11 | Name/trademark dispute | Low | Medium | IP India search before spending on brand; backups TableLoop / ServeLoop (see AGENTS.md) |

## Kill criteria

Review on a fixed calendar. If any "kill" line is hit, stop new sales and either pivot or shut down DineLoop and move core work to another CraftLayer vertical.

| Checkpoint | Continue if | Pivot or kill if |
|---|---|---|
| Week 8 (MVP done) | 3+ pilot outlets live, 30%+ of their dine-in orders via QR | Fewer than 2 outlets willing to run real service on it |
| Month 4 | 10+ paying outlets, at least 4 on Growth | Under 5 paying outlets after 60+ in-person demos |
| Month 6 | 25+ paying outlets, monthly logo churn ≤ 5%, ≥ 20% phone capture | Churn > 8%/month or phone capture < 10% (CRM thesis fails) |
| Month 9 | MRR ≥ ₹75,000, CAC payback ≤ 9 months | MRR < ₹30,000 or payback > 15 months |
| Month 12 | MRR ≥ ₹2 lakh, net revenue retention ≥ 100% | MRR < ₹75,000: pivot to "CRM + WhatsApp add-on for Petpooja users" only, or kill |

Pivot options before killing: (a) drop ordering, sell only the CRM/review/WhatsApp layer as a plug-in for existing POS; (b) sell white-label to a POS company; (c) narrow to bars/pubs where AOV and repeat rates are highest.
