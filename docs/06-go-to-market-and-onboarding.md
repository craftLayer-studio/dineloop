# 06 — Go-to-market and onboarding

## Strategy in one paragraph

Win one city cluster with founder-led, in-person sales to independent cafes and casual-dining restaurants that already feel aggregator and staffing pain. Lead with a free 14-day pilot that runs real Saturday service, prove three numbers (QR order share, diners captured, Google reviews added), then convert to annual Growth. Use each live outlet as a showroom for its neighbours on the same street. Add field reps once the first 10 are paying and the script is proven.

## MVP timeline (6–8 weeks to sellable)

Builds on TableTap M0 (see [01-product-plan.md](01-product-plan.md#existing-codebase-tabletap)).

| Week | Build | Sell (in parallel) |
|---|---|---|
| 1–2 | TableTap M1: Postgres + RLS, staff OTP login and roles, menu editor, QR sheet, SSE | 30 owner interviews; pick launch street/area; shortlist 10 pilot targets |
| 3–4 | TableTap M2: Razorpay/Cashfree test mode, webhooks, cash by staff, GST bill with FSSAI number | Sign 3 pilot LOIs (free 14 days, then ₹24,999/yr Growth) |
| 5–6 | Core CRM: OTP phone capture, DPDP notice, consent ledger; WhatsApp bill (utility); review funnel | Pilot 1 live (soft launch, weekday dinner) |
| 7–8 | WhatsApp campaigns with 5 templates, owner dashboard v2, onboarding wizard | Pilots 2–3 live; first conversions; start sales to next 20 |

Cut list if late: itemised split, sound alerts, Hindi menu, segment builder. Never cut: consent ledger, real payments, staff confirm.

## Channels (ranked for the first 12 months)

| Rank | Channel | Cost | Why |
|---|---|---|---|
| 1 | Founder walk-ins, 3–5pm (owner free, outlet quiet) | Time | Restaurant owners buy on trust and demos |
| 2 | Street clustering: after one live outlet, pitch every cafe within 1 km with "go see it at X" | Low | Social proof is local |
| 3 | Referrals from live owners (1 month free per referral) | Low | Owners know other owners |
| 4 | Local restaurant associations (NRAI chapters, city hotel associations), food-business WhatsApp groups | Low | Credibility; aggregator anger is the shared topic |
| 5 | Instagram reels: "How [cafe] got 312 Google reviews in 60 days" | Low–medium | Owners watch competitor reels (the TableTap idea itself came from one) |
| 6 | Partnerships: restaurant consultants, interior designers, CA firms, kitchen equipment dealers | Revenue share 10–15% of year-1 | They meet owners at opening, the best trigger moment |
| 7 | Google Ads on "QR menu", "Petpooja alternative" | Medium | Only after conversion funnel is proven |

## First 10 paying customers — exact plan

1. **Pick one area** with 50+ cafes within 3 km (for example Koramangala/Indiranagar in Bengaluru, Baner/Koregaon Park in Pune, Vijay Nagar in Indore). Write the list from Google Maps: name, rating, review count, Zomato listing, owner name.
2. **Prioritise** outlets with: 4.0–4.3 Google rating and under 500 reviews (review funnel has visible upside), active on Zomato/Swiggy (commission pain), 10–40 tables, owner visible on Instagram.
3. **Visit 5 outlets a day, 3–5pm.** Use the 5-minute script below. Leave a printed QR standee with a demo menu of *their own* top 10 dishes (prepare from Zomato menu the night before).
4. **Offer the pilot:** free 14 days, we set up everything in one hour, we stand in the outlet on the first Friday and Saturday night.
5. **During pilot** send the owner a WhatsApp summary every night: orders via QR, diners captured, reviews added.
6. **Day 12 close meeting:** show the three numbers; ask for annual Growth at ₹24,999 (setup waived). Fallback: monthly Growth ₹2,499. Last fallback: Starter.
7. **Ask every converted owner for two intros** the same day.

Math: ~60 walk-ins → ~15 pilots (25%) → ~10 paid (65%) over roughly 6 weeks (estimate).

## Sales script (5 minutes, Hindi/English mix as needed)

1. **Open with their number.** "Your Google rating is 4.1 with 280 reviews. Cafe X next door has 1,100. Want to see how to get 20 new reviews every month without asking anyone?"
2. **Pain probe (pick two).** "How much do you pay Zomato each month?" "How many waiters left this year?" "Do you know the phone numbers of your top 100 regulars?"
3. **Demo on their own menu.** Hand the phone: scan, order, the kitchen screen updates on a second phone, pay, review prompt goes to *their* Google page.
4. **The loop.** "Every table that scans gives you a customer you own. Next Tuesday you WhatsApp 500 of them a 'Tuesday biryani' offer. Cost: about ₹1 per message."
5. **Price against pain.** "₹2,083 a month on annual. That is one Zomato order's commission per day. Or two extra tables a month."
6. **Close the pilot.** "We set it up tomorrow at 4pm, free for 14 days, and I'll be here Saturday night. If your staff hate it, we take it away."

## Objection handling

| Objection | Response |
|---|---|
| "I already have Petpooja." | "Keep it. DineLoop sends QR orders into Petpooja (P1) and adds what Petpooja charges ₹10,000–20,000 extra for: CRM, WhatsApp, reviews. You'll pay less than their marketing bundle." |
| "My customers won't scan." | "They don't have to. Waiters still take orders on the same system. In the pilot we'll measure how many do. Most groups under 40 scan." |
| "Free QR menus exist." | "Those show a PDF. This takes the order, sends it to the kitchen, collects UPI and gets you the diner's number with permission. The menu is free; the customer is the product." |
| "WhatsApp marketing is spam." | "We only message diners who ticked yes, max 4 a month, with STOP to leave. That's also the law under DPDP." |
| "Too expensive." | "Starter is ₹833 a month. Growth pays for itself with 7 extra visits a month. We'll show you the number in your dashboard." |
| "My staff are not tech-savvy." | "The waiter does one tap per order: confirm. We train them in 20 minutes during the pilot." |
| "What if internet goes down?" | "Waiters switch to paper KOT; orders already placed stay on screen. Printer fallback is coming." |
| "Will Zomato punish me?" | "We never touch Zomato orders or packaging. We just help diners who already sat at your table come back directly." |
| "Let me think." | "Let's book the free pilot for next Thursday; you can cancel anytime before. No card needed." |

## Onboarding checklist (target: live in 1 visit, ≤ 90 minutes)

### Before the visit (remote, 30 minutes)

- [ ] Account created; outlet name, city, address, GSTIN, FSSAI licence number, GST rate (5% or 18%) recorded
- [ ] Menu imported from Zomato/Swiggy listing, PDF or photo; owner confirms prices on WhatsApp
- [ ] Items tagged veg/non-veg, spice, allergens, station (kitchen/bar/dessert), prep minutes
- [ ] Tables and sections defined from owner's count; QR sheet generated and standees printed
- [ ] Google Business Profile review link fetched
- [ ] Payment account: Razorpay/Cashfree sub-merchant KYC started (PAN, GSTIN, bank, cancelled cheque), UPI VPA as fallback
- [ ] WhatsApp sender decided: DineLoop shared number (default) or owner's own WABA (Growth+)
- [ ] DPA (data processing agreement) and terms e-signed; privacy notice personalised with outlet name

### On-site (60 minutes, before evening service)

- [ ] Place QR standees on every table; test-scan each one
- [ ] KDS on kitchen tablet/TV; bar station if any; volume up
- [ ] Waiter app on 1–2 staff phones; logins created by role
- [ ] Run 3 test orders end to end: scan → staff confirm → KDS → ready → served → bill → split → pay → review
- [ ] Train waiters (20 min): confirm, serve, mark cash, handle "can't scan" diners
- [ ] Train chef (10 min): start, ready, late highlight
- [ ] Owner dashboard on owner's phone; daily WhatsApp summary switched on
- [ ] Table tent copy: "Scan to order and pay. Get your bill on WhatsApp."

### First 14 days

- [ ] Day 1 and first Saturday: be on site during peak
- [ ] Daily summary to owner: QR order share, diners captured, opt-in rate, reviews added
- [ ] Day 3: fix menu errors, add photos for top 10 dishes
- [ ] Day 7: send first WhatsApp campaign together (win-back or weekend offer) to opted-in diners
- [ ] Day 10: switch on game (Growth pilots)
- [ ] Day 12: close meeting with results sheet

## Activation metrics (per outlet)

| Milestone | Target day |
|---|---|
| First live QR order | Day 1 |
| 100 QR orders | Day 7 |
| 100 diners captured | Day 10 |
| First campaign sent | Day 7 |
| 20 new Google reviews | Day 30 |

## Retention playbook

| When | Action | Owner of action |
|---|---|---|
| Weekly | WhatsApp digest to owner: revenue, QR share, diners, reviews, campaign revenue | Automated |
| Monthly | "Your DineLoop ROI" card: campaign revenue vs fee | Automated |
| Day 30 | Check-in call; suggest next campaign and loyalty setup | Customer success |
| Day 60 | Upsell review: Starter → Growth if 500+ diners; done-for-you if < 1 campaign/month | Customer success |
| Festivals (Diwali, Christmas, New Year, IPL) | Ready-made campaign templates and creatives sent 10 days before | Marketing |
| Usage drop (QR share < 20% for 7 days) | Alert to CS; on-site re-training visit | Customer success |
| 45 days before annual renewal | ROI report + renewal offer (2 months free if prepaid early) | Customer success |

Health score (estimate weights): QR order share 30%, campaigns sent last 30 days 25%, owner dashboard logins 20%, diner capture 15%, support tickets (inverse) 10%. Red accounts get a visit within 7 days.

## Hiring sequence

| Paying outlets | Hire |
|---|---|
| 10 | Field sales rep #1 (from F&B background: ex-Zomato/Swiggy account manager ideal) |
| 30 | Onboarding + support specialist (Hindi + local language) |
| 60 | Field sales rep #2; second area in same city |
| 100 | Customer success lead; second city |
