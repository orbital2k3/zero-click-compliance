# ZCC Go-to-Market Plan

**Date:** 2026-08-18 · **Horizon:** 12 months from launch · **Companion docs:** [project-review.md](project-review.md) · [business-plan.md](business-plan.md)

Tags: 🟢 verified · 🟡 industry estimate · 🔴 assumption to validate.

---

## 1. The four questions this plan answers

1. **Who are we for?** GRC analysts and vCISOs who must review vendor SOC 2 reports and hate it.
2. **Why do they choose us?** The only tool that reads a SOC 2 like a senior auditor — opinion, graded exceptions, CUECs, with page-level citations — in minutes for $49, without buying a platform.
3. **How do they find us?** Content-led PLG: rank for the searches analysts already make, seed the communities they already trust, and let a $49 credit-card purchase do the selling. Partner with vCISO firms as the force multiplier.
4. **Is it working?** Visitor→purchase ≥1.5%, repeat purchase ≥30%, CAC payback <3 months on every channel. Kill criteria are explicit (§8).

## 2. ICP and segmentation

**Primary ICP — "the drowning GRC analyst":** security/GRC person (often a team of 1–3) at a 100–1,000 employee company that holds its own SOC 2/ISO cert and must run vendor reviews to keep it. Has 50–300 vendors 🟡, reviews are backlogged, renewal season is a fire drill. Buys with a corporate card; $49 needs no approval.

**Second ICP — "the leverage buyer": vCISO / MSSP / compliance consultancy.** Reviews reports across many clients; time is literally billable. One firm = 50–500 reports/yr 🟡. Fastest path to volume and the core of the partner motion (§6).

**Explicitly NOT the ICP in year 1:** Fortune 1000 TPRM programs (procurement cycles, security reviews we can't yet pass), and companies with no compliance obligations (no burning need).

**Trigger moments to target:** own SOC 2 audit approaching (auditor asks for vendor-review evidence) · new vendor in procurement · annual report refresh · post-incident vendor scrutiny · new GRC hire inheriting a backlog.

## 3. Positioning & messaging

**Category framing:** don't invent a category; steal a job. ZCC is **"vendor SOC 2 review, done in minutes"** — a job-to-be-done wedge inside TPRM, positioned as a *complement* to Vanta/Drata ("keep your platform; we read the PDFs it collects").

**Positioning statement:** *For security teams who have to review vendor SOC 2 reports, ZCC is the AI analyst that turns a 150-page audit PDF into a graded risk decision in minutes — unlike GRC platforms that collect documents but leave the reading to you.*

**Messaging architecture:**

| Pillar | Message | Proof |
|---|---|---|
| Speed | "8 hours of reading → 10 minutes" | Live demo on a public SOC 2 (e.g., a vendor's freely shared report) |
| Depth | "We don't summarize — we extract the opinion, every exception with severity, and your CUECs" | Sample report; side-by-side vs. ChatGPT summary |
| Trust | "Your vendor's report never trains a model and is deleted after processing" | Trust page, DPA, deletion guarantee; page-level citations for every finding |
| Price | "$49. No demo call. No platform." | The checkout page itself |

**Objection pre-emption (must be on the landing page):** "Can I even upload this? It's under NDA." → answer with the zero-retention/deletion posture up front. This is the #1 conversion blocker to test. 🔴

## 4. Growth model: content-led PLG with a partner overlay

Sales-led is wrong at a $49 entry point; pure viral PLG is wrong for a compliance chore. The fit is **content/SEO-led self-serve** (analysts search for exactly this pain), plus a **partner motion** for the vCISO multiplier. ACV math: even Pro tier ($399/mo) doesn't support human-touch sales; nothing in year 1 requires a sales hire.

**Growth loops:**
1. **Deliverable loop:** every ZCC report is a branded DOCX that lands in front of the analyst's boss, their auditor, and sometimes the vendor — each report is an ad in the exact right room.
2. **Renewal loop:** SOC 2 reports expire annually → expiry reminders → recurring usage without reacquisition.
3. **Content loop:** anonymized corpus stats ("we analyzed 1,000 SOC 2 reports; 34% had exceptions; here are the 10 most common" 🔴) → the definitive data-driven content in a space full of thin listicles → links, rankings, trust.

## 5. Channels (with CAC hypotheses)

| Channel | Play | 12-mo expectation | CAC hypothesis |
|---|---|---|---|
| **SEO/content** (lead) | Own "how to read a SOC 2 report," "SOC 2 exceptions examples," "CUEC checklist," "qualified opinion meaning," vendor-review templates. 2 deep posts/mo + free tools (CUEC extractor, review checklist) | 6–10K organic visits/mo by month 12 🔴 | Near-$0 marginal; founder time |
| **Communities** | Genuine participation: r/GRC, r/cybersecurity, GRC Slack/Discord groups, LinkedIn GRC voices. Share the corpus-stats content, not ads | Spiky, high-intent bursts | ~$0; reputation-priced |
| **Partnerships (vCISO/MSSP)** | 20% revenue share or volume pricing; co-branded reports; "powered by ZCC" | 5 firms live; 25–40% of report volume 🔴 | Lowest CAC per report at scale |
| **Launch moments** | Product Hunt + Hacker News ("Show HN: AI that reads SOC 2 reports") + LinkedIn founder posts | 2–5K visits each, backlinks | ~$0 |
| **Paid search** (test only, month 6+) | Bottom-funnel terms ("soc 2 report review service") — tiny budget ($1–2K/mo) purely to read intent pricing | Data, not volume | Must show <$150 CAC per subscriber or kill 🔴 |
| **Auditor/CPA firms** (opportunistic) | Firms whose clients ask "what do I do with my vendors' reports?" | 1–2 referring relationships | ~$0 |

**What we deliberately don't do in year 1:** outbound SDR motion, events/booths, brand advertising, and any channel whose payback can't be measured inside a quarter.

## 6. Partner motion detail (the multiplier bet)

vCISO firms are the one segment where a single deal changes the volume curve. Offer: Pro tier at partner pricing, white-label-ish report headers (their logo alongside ZCC's), and margin on client billings. Ask: 3 design-partner firms pre-launch (free), converting to paid at launch. Success metric: a partner firm running ≥20 reports/mo by month 9. 🔴 If two firms hit that, partner channel becomes the primary growth investment for year 2.

## 7. Funnel math (base case, month 12 steady state)

Working backward from the business plan's $12K MRR base case:

```
10,000 visits/mo
  × 1.5% visitor → paid report          = 150 first/repeat purchases/mo 🔴
  30% of purchasers repeat within 60d                                🔴
  × 20% of repeaters → subscription      = ~6–8 new subscribers/mo    🔴
  + partner channel ≈ 30% of report volume on top
→ ~120 one-off reports/mo ($5.9K) + ~35 subscribers ($6.3K at $180 blended) ≈ $12K MRR
```

Every number tagged 🔴 gets a real value within 60 days of launch; the funnel model is rebuilt monthly from actuals.

## 8. Launch plan & phase gates

**Phase 0 (pre-launch, months 0–3): private beta.**
Design partners (10) run real reports free. Deliverables: accuracy benchmark published, trust page live, 3 testimonials, landing page conversion-tested against the NDA objection.
*Gate:* partners rate output "usable without re-reading the PDF" ≥80%. Fail → fix product, don't launch.

**Phase 1 (months 3–6): public launch.**
Product Hunt + Show HN + LinkedIn within one week; corpus-stats flagship post; communities seeded. Target: 100 cumulative paid reports, 10 subscribers, $2.5K MRR.
*Gate:* repeat-purchase ≥30%. Fail → the product is a one-shot novelty; diagnose before spending on traffic.

**Phase 2 (months 6–12): compound.**
SEO library to 20+ assets; paid-search test; 5 partner firms live; autonomous-outreach feature launch as the second PR moment ("the report chases itself"). Target: $10K+ MRR.
*Gate:* at least one channel with CAC payback <3 months and month-over-month volume growth → that channel gets 70% of effort in year 2.

**Kill criteria (honesty clause):** <100 total paid reports by month 6, or repeat rate <15% after fixes → the wedge hypothesis is wrong. Fall back to the two documented alternatives: consultant-only tooling (ICP 2 only), or pivot to the CAIA/AI-governance thesis with learnings and cash intact.

## 9. Marketing budget (12 months)

Total: **~$15–20K cash** (founder time is the real spend).

| Item | Budget |
|---|---|
| Design/brand polish for reports + site | $4K |
| Content editing/design support | $4K |
| Paid search experiment (months 6–9) | $5K |
| Tools (analytics, SEO, email) | $2K |
| Community/launch misc | $2K |

## 10. GTM metrics dashboard (weekly)

| Metric | Healthy |
|---|---|
| Organic visits / top-5 keyword rankings | +10% m/m after month 4 |
| Visitor → purchase | ≥1.5% |
| Landing → checkout start (NDA-objection proxy) | ≥6% 🔴 |
| Repeat purchase (60d) | ≥30% |
| Purchaser → subscriber | ≥20% of repeaters |
| Partner-sourced report share | 25%+ by month 12 |
| CAC payback (any paid channel) | <3 months |
| NPS from report recipients | >40 |
