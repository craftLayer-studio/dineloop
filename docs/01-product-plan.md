# 01 — Product plan

## Vision

Make every Indian restaurant's best customers *its own* customers, not Zomato's or Swiggy's. DineLoop turns each table, bill and delivery bag into a doorway into a consented diner database, then uses that database to bring the diner back directly. Within three years: the default "guest growth" layer for independent restaurants in Tier 1–3 India, then Gulf and South-East Asian markets with similar UPI/WhatsApp behaviour.

North-star metric: **repeat direct orders per outlet per month** (dine-in revisits from campaigns + direct online orders). It proves both retention for the owner and stickiness for us.

## Ideal customer profile

| Attribute | Target |
|---|---|
| Format | Independent cafe, casual dining, bar/pub, family restaurant; later QSR, food courts, cloud kitchens |
| Size | 8–40 tables, ₹4–40 lakh monthly revenue (estimate: ₹1,200 AOV x 30–120 bills/day) |
| Location | Tier 1–2 city cluster first (for example Pune, Indore, Jaipur, Bengaluru suburbs), Tier 3 after 100 customers |
| Tech today | Petpooja/other POS or paper billing; Zomato/Swiggy listed; WhatsApp Business app used manually |
| Decision maker | Owner-operator, aged 25–45, present in the outlet most evenings |
| Trigger events | New outlet opening, waiter shortage, aggregator commission pain, falling Google rating, slow weekdays |

Anti-ICP (do not sell in year one): fine-dining with sommelier-led service, dhabas with no smartphone-using guests, chains over 20 outlets that need ERP-grade procurement.

## Personas

| Persona | Goal | Frustration | What DineLoop gives |
|---|---|---|---|
| Rohit, cafe owner (2 outlets, Pune) | Fill weekday tables, stop paying 25% to aggregators | No idea who his regulars are; staff quit every 3 months | CRM of diners, WhatsApp win-back, direct ordering link |
| Meena, restaurant manager | Smooth service on Saturday night | Wrong orders, angry tables, lost KOTs | QR orders straight to KDS, floor map, waiter calls |
| Imran, head chef | Cook in order, waste less | Handwritten KOTs, no prep timing, over-ordering stock | Station KDS with timers, recipe costing (P2) |
| Arjun, waiter/captain | Serve more tables, earn tips | Running back and forth for menus and bills | Live table states, tips shown per waiter |
| Priya, diner (28, Bengaluru) | Order fast, split with friends, pay by UPI | Waiting for menu, waiter, bill | Scan, order, play, split, pay in under a minute |

## User journeys

### Diner, dine-in (the core loop)

1. Sits down, scans table QR. Menu opens in the browser in under 2 seconds on 4G (no app, no login).
2. Browses with veg/allergen filters, sees chef picks and combos. Upsell prompt: "Add a mojito for ₹149?"
3. Places order. Optional phone OTP step: "Get your bill and order updates on WhatsApp" with a DPDP notice and an unticked marketing opt-in box.
4. Sees live status ("cooking, ready in about 12 min"). While waiting, plays a 30-second game (spin wheel, scratch card, quiz) and may win a coupon valid on the *next* visit.
5. Calls waiter or orders more from the same page.
6. Requests bill, splits evenly or by item, adds tip, pays by UPI. Gets the GST bill on WhatsApp (utility template).
7. Rates the meal. 4–5 stars: one tap to the restaurant's Google review page. 1–3 stars: private feedback to the owner, who gets an alert to recover the guest.
8. Days later: birthday offer, "we miss you" win-back after 30 days, or the coupon won in the game, all via WhatsApp to opted-in diners only.

### Owner

1. Signs up with a sales rep, menu imported from a photo/PDF/Petpooja export in the onboarding session.
2. Prints QR standees (we ship them), sets tables and sections, GST rate, UPI/payment account.
3. Watches the live floor map and day summary on phone.
4. Each week: sees new diners captured, repeat rate, reviews gained, campaign revenue. Sends one-tap campaigns from templates.
5. Month 2+: switches on direct ordering link and shares it in Instagram bio, Google Business Profile and the delivery bag insert.

### Kitchen and waiter

KDS shows orders by station with elapsed timers and late highlighting; chef taps start/ready. Waiter app shows floor map (free, ordering, eating, needs help, bill requested), confirms each guest order with one tap before the kitchen sees it, and marks served.

## Existing codebase (TableTap)

The founder's prototype **TableTap** ([github.com/craftLayer-studio/tabletap](https://github.com/craftLayer-studio/tabletap), accessed 2026-11-24) is DineLoop's ordering module. It is Next.js App Router + TypeScript, with pure domain rules in `src/domain/` (unit tested with Vitest), an in-memory store in `src/server/store.ts`, polling every 2.5 s and simulated payments. Its `PLAN.md` defines the Postgres data model, the order state machine (`placed → confirmed → cooking → ready → served`, with cancel), multi-tenancy with row-level security, SSE realtime and payment rules. Milestones: M0 prototype (done), M1 Postgres + auth, M2 payments, M3 pilot.

### Coverage of DineLoop MVP features

| DineLoop MVP feature | TableTap status | Gap to close |
|---|---|---|
| Table QR menu with veg mark, allergens, spice, half/full, deals, sold out | Done (M0) | QR image generation, signed rotatable table tokens, real photos (M1) |
| Cart, notes, place order | Done | Item modifiers (extra cheese), combos |
| Staff confirms order before kitchen | Done | Optional auto-confirm per outlet |
| KDS by station with timers and late highlight | Done (per order) | Per-item station status, sound alerts, KOT printer output |
| Live order status and ETA | Done | None for MVP |
| Call waiter / request bill | Done | Push or sound alert on staff phones |
| Live floor map | Done | Sections, table merge/transfer |
| GST bill, tip, even split, UPI intent link | Done, **simulated** payments | Real gateway with webhooks (Razorpay/Cashfree), staff-confirmed cash, itemised split, GST-compliant invoice format with FSSAI number |
| One-tap review after payment | Done (internal rating) | Route 4–5 stars to Google review link; 1–3 stars to owner alert |
| Owner day summary | Done (since IST midnight) | Date ranges, export, weekly digest on WhatsApp |
| Persistent data, multi-tenant | **Missing** (in-memory) | Postgres + RLS per PLAN.md M1 |
| Staff login and roles | **Missing** (no auth) | OTP login, roles owner/manager/waiter/kitchen (M1) |
| Menu editor for owners | **Missing** | Menu editor + import from photo/PDF/CSV |
| Diner phone capture with DPDP consent | **Missing** | OTP capture, consent ledger, opt-out (core CRM module) |
| Diner CRM (profiles, visits, spend, tags) | **Missing** | Core CRM module, linked to `table_sessions` and `bills` |
| WhatsApp messaging (bill, campaigns, birthday, win-back) | **Missing** | Core WhatsApp module on Cloud API via BSP |
| Wait-time games and coupons | **Missing** | Core games module, coupon ledger |
| Loyalty points / stamps | **Missing** | Core loyalty module |
| Direct online ordering (delivery/takeaway) | **Missing** | Storefront page, delivery zones, Shadowfax/Porter/own riders hand-off |
| Aggregator integration (Zomato/Swiggy) | **Missing** | Via Petpooja/UrbanPiper middleware first; direct APIs later |
| POS integration (Petpooja, Posist) | **Missing** | Push orders to POS, pull menu |
| Inventory, recipe costing | **Missing** | P2 |
| Multi-outlet | **Missing** | P2 |

Rough estimate: TableTap covers about 60% of P0 ordering/KDS scope and 0% of the CRM/marketing scope that justifies Growth pricing (estimate, counted by P0 rows above). The MVP plan below finishes TableTap M1–M2 and adds the guest-revenue layer.

## Features by phase

Priority key: P0 = MVP, sellable in 6–8 weeks. P1 = months 3–6. P2 = months 6–12. Each feature names the metric it moves.

### P0 — MVP (weeks 1–8)

| Feature | Source | Metric | Target |
|---|---|---|---|
| Postgres + RLS + staff OTP login and roles | TableTap M1 | Activation (production-ready) | 0 cross-tenant leaks in tests |
| Menu editor + menu import (CSV, photo via OCR-assisted entry) | New | Activation | Menu live in under 60 min |
| QR standee sheet generator, rotatable table tokens | TableTap M1 | Activation | All tables live on day 1 |
| QR order, KDS, waiter app, floor map, call waiter | TableTap M0 | Retention (ops value) | 40%+ of dine-in orders via QR by week 4 (estimate) |
| Real payments: UPI via gateway with webhooks, cash by staff | TableTap M2 | Revenue (payment share) | 50%+ of bills paid in-app (estimate) |
| Phone capture by OTP with DPDP notice and separate marketing opt-in | Core CRM | Retention | 25%+ of tables capture a phone (estimate) |
| Diner CRM list: visits, spend, last visit, birthday | Core CRM | Retention | — |
| Bill on WhatsApp (utility template) | Core WhatsApp | Retention | Delivery rate 95%+ |
| Google review funnel (4–5 stars to Google, 1–3 private) | Core reviews | Acquisition | +20 Google reviews per outlet in month 1 (estimate) |
| WhatsApp campaign sender with 5 templates (win-back, birthday, weekday offer, new dish, event) | Core WhatsApp | Revenue, retention | 3%+ redemption per campaign (estimate) |
| Owner dashboard: today, week, diners captured, reviews, campaign revenue | TableTap M0 + core analytics | Retention (owner sees ROI) | Weekly active owners 80%+ |

### P1 — months 3–6

| Feature | Metric | Why |
|---|---|---|
| Wait-time mini-games (spin, scratch, quiz) with next-visit coupons | Retention, capture rate | Gives diners a reason to share a phone number; coupon pulls a revisit |
| Loyalty: points per ₹100 or visit stamps, wallet on WhatsApp | Retention | Standard ask from cafe owners; Petpooja sells it in Marketing Manager |
| Direct online ordering site (takeaway + delivery) with 0% commission, own delivery or Porter/Shadowfax/Dunzo-style hand-off | Revenue (owner margin), ARPU | Moves repeat delivery customers off aggregators |
| Smart upsell: pairings, combos, "most ordered with", time-based deals | Revenue (AOV) | Vendor data shows 12–30% AOV lift from QR ordering (see 04) |
| Itemised split and pay-per-person | Activation | Groups of friends are the core cafe crowd |
| GST billing module (POS-lite): KOT print, bill print, day close, GSTR-1 export | ARPU, activation for no-POS outlets | Lets us replace paper billing |
| Petpooja / Posist order push integration | Activation (removes double entry) | Owners will not re-key orders |
| Hindi + regional language menus | Activation in Tier 2–3 | Planned in TableTap |
| Segment builder (spent > ₹X, not visited in Y days, loves desserts) | Revenue | Better campaign targeting |

### P2 — months 6–12

| Feature | Metric | Why |
|---|---|---|
| Inventory, recipe costing, wastage log, low-stock alerts | ARPU (Pro) | Food cost is the largest input cost for operators (see 04) |
| Multi-outlet dashboard, central menu, cross-outlet CRM | ARPU, expansion | Chains of 3–20 outlets |
| Aggregator order sync (via UrbanPiper-style middleware) and reconciliation | ARPU | One screen for all orders |
| Staff attendance, shift roster, tip distribution | Retention | Attrition is high; tips motivate |
| Table reservations and waitlist with WhatsApp "your table is ready" | Revenue | Weekend turnover |
| Self-order kiosk mode for QSR/food courts | Acquisition (new segment) | Food court tokens |
| AI menu insights ("paneer tikka margin falling, raise ₹20") | ARPU | Differentiator for Pro |
| Referral program for diners ("give ₹100, get ₹100") | Referral | Viral loop |

## Data model (additions to TableTap PLAN.md)

TableTap's tables (`restaurants`, `staff_users`, `tables`, `table_sessions`, `menu_*`, `orders`, `order_items`, `order_status_events`, `service_requests`, `bills`, `bill_shares`, `payments`, `reviews`) stay as defined. All money is integer paise; every tenant row has `restaurant_id` with Postgres RLS. DineLoop adds:

```
brands             id, name, owner_user_id                       -- groups outlets (restaurants) for multi-outlet
diners             id, brand_id, phone_e164, name, birthday, anniversary, first_seen_at, last_seen_at,
                   visits, lifetime_spend_paise, tags[]
consents           id, diner_id, purpose (bill_updates|marketing|loyalty|reviews), granted bool,
                   notice_version, channel (qr_web|whatsapp|staff), captured_at, withdrawn_at, ip_hash
diner_sessions     diner_id, table_session_id                      -- links a visit to a diner
coupons            id, brand_id, code, kind (percent|flat|free_item), value, min_bill_paise,
                   valid_from, valid_to, source (game|campaign|loyalty|manual), diner_id, redeemed_at, bill_id
game_plays         id, table_session_id, diner_id, game (spin|scratch|quiz), prize_coupon_id, played_at
loyalty_ledger     id, diner_id, outlet_id, points, reason (earn|redeem|expire|adjust), bill_id, created_at
campaigns          id, brand_id, name, template_id, segment_json, scheduled_at, status, sent, delivered, read, redeemed
messages           id, campaign_id, diner_id, wa_message_id, category (marketing|utility|service),
                   cost_paise, status, sent_at
wa_credits_ledger  id, brand_id, delta_paise, reason (topup|send|refund), created_at
feedback           id, review_id, routed_to (google|owner), resolved_by, resolved_at
online_orders      id, restaurant_id, diner_id, type (takeaway|delivery), address_json, delivery_fee_paise,
                   rider_ref, status                                -- extends orders
recipes (P2)       menu_item_id, ingredient_id, qty, unit
ingredients (P2)   id, restaurant_id, name, unit, cost_paise, stock_qty, reorder_level
```

Rules: a diner record exists per brand, not globally across CraftLayer customers (purpose limitation; never share diners between restaurants). Marketing sends query `consents` where `purpose = marketing and granted and withdrawn_at is null`. "STOP" replies on WhatsApp set `withdrawn_at` within one minute.

## Integrations

| Integration | Phase | Purpose |
|---|---|---|
| Razorpay or Cashfree (split settlement to outlet) | P0 | UPI/card payments with webhooks |
| WhatsApp Cloud API via a BSP (Gupshup, Interakt, AiSensy or direct Meta) | P0 | Bills, campaigns, OTP fallback |
| SMS OTP provider (MSG91 etc.) with DLT templates | P0 | Phone verification |
| Google Business Profile review link | P0 | Review funnel (deep link, no API needed) |
| Petpooja / Posist APIs | P1 | Push QR orders into existing POS |
| Thermal KOT printers (ESC/POS via local print bridge) | P1 | Kitchens that still want paper |
| UrbanPiper or direct Zomato/Swiggy APIs | P2 | Aggregator order sync |
| Porter / Shadowfax / own riders | P1 | Direct delivery fulfilment |
| Tally / GST export | P1 | Accountant handoff |

## Metrics

| Layer | Metric | Healthy target (estimate) |
|---|---|---|
| Activation | Days from payment to first live QR order | ≤ 3 days |
| Usage | Share of dine-in orders placed by QR | ≥ 40% by day 30 |
| Data | Share of tables with a verified diner phone | ≥ 25% |
| Data | Marketing opt-in rate among captured diners | ≥ 50% |
| Owner value | Google reviews added per month | ≥ 20 |
| Owner value | Campaign-attributed revenue per month | ≥ 5x DineLoop fee |
| Revenue | ARPU (blended) | ≥ ₹2,000/month |
| Retention | Logo churn | ≤ 3% per month |
| Expansion | Starter → Growth upgrade within 90 days | ≥ 30% |
