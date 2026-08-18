# ZCC Business Plan

**Zero Click Compliance — AI-powered vendor SOC 2 analysis**
**Date:** 2026-08-18 · **Stage:** Pre-revenue MVP · **Companion docs:** [project-review.md](project-review.md) · [go-to-market-plan.md](go-to-market-plan.md)

Figures are tagged: 🟢 verified · 🟡 industry estimate · 🔴 assumption to validate with customers.

---

## 1. Executive summary

Every company that takes security seriously must review the SOC 2 reports of its vendors — and those reports are 100–200 page PDFs written by auditors for auditors. A GRC analyst spends 2–8 hours per report 🟡, hundreds of times a year at a mid-size company. It is one of the most hated, most skipped, and most audit-visible chores in security.

**ZCC turns a SOC 2 Type II report into a structured risk decision in minutes**: auditor opinion, every exception graded by severity, subservice organizations, and the Complementary User Entity Controls the customer is actually on the hook for — delivered as a clean report for $49.

- **Wedge:** $49 pay-per-report, self-serve, credit card. No sales call, no platform migration, below most expense-approval thresholds.
- **Expansion:** subscription tiers add a vendor portfolio, continuous monitoring (reports age out annually), autonomous vendor outreach (the original "zero click" vision), and team/API features.
- **Endgame:** the system of record for third-party assurance analysis — the layer that reads what vendors send, regardless of which GRC platform the customer runs.

The MVP is built (React + Express + Supabase + Stripe + model-agnostic LLM analysis, ~4,400 LOC 🟢). The plan below targets **$10K MRR within 12 months on a bootstrap/pre-seed budget**, with a decision gate at that point on raising a seed round.

## 2. Problem

1. **Volume:** A 200-person SaaS company typically has 100–300 vendors 🟡; SOC 2 review is required for the security-relevant ones at onboarding *and* annually thereafter.
2. **Expertise scarcity:** Reading an auditor's opinion correctly (qualified vs. unqualified, carve-outs, exception materiality) is specialist work; most teams have one person who can do it, and that person is a bottleneck.
3. **Theater:** Because it's slow, many teams "review" reports by filing them. This is invisible until *their* auditor or a breach exposes it.
4. **Existing tools don't solve it:** GRC platforms (Vanta, Drata) automate *your own* compliance and vendor questionnaires; security-rating tools (SecurityScorecard) scan external surfaces. The actual reading of the assurance document a vendor hands you remains manual almost everywhere. 🟡

## 3. Product

### Today (built 🟢)
Upload a SOC 2 Type II PDF → AI extracts a Zod-validated structure: report type, trust criteria, audit period, auditor firm, opinion + summary, subservice organizations (carve-out/inclusive), exceptions with vendor responses and AI-graded severity (LOW→CRITICAL), and CUECs → generated DOCX report → $49 via Stripe.

### Near-term roadmap (0–6 months)
- **Source-linked findings:** every extracted claim links to the PDF page (trust + accuracy defense).
- **Vendor portfolio dashboard** (largely built): status, severity rollup, report expiry dates.
- **Re-review reminders:** SOC 2 reports expire annually — recurring revenue is built into the domain.
- **Bridge-letter and SOC 3 handling; ISO 27001 certificate parsing** as fast-follow document types. 🔴 *validate demand*

### Later (6–18 months, subscription drivers)
- **Autonomous outreach:** enter `security@vendor.com`; ZCC requests the report, receives the reply, ingests the attachment (email plumbing already exists in `emailService.ts` 🟢).
- **Cross-portfolio intelligence:** "3 of your vendors carve out the same subservice DC provider."
- **API + integrations:** push results into Vanta/Drata/Jira/Slack — position as complement, not rip-and-replace.
- **Expansion thesis on file:** AI-governance/CAIA compliance for insurance (see `competition_analysis.md`) — parked until ~$25K MRR or a pulling design partner. 🔴

## 4. Market

- **TPRM software market:** ~$8B globally, growing ~15%/yr 🟡. ZCC's serviceable slice is the *assurance-document analysis* layer, not the whole category.
- **Bottom-up SAM:** ~50K–100K companies in North America + EU run formal vendor security review programs (roughly: companies with a compliance framework of their own — Vanta + Drata alone claim ~30K customers combined 🟡). At 30 reviewed vendors/yr average × $49–99 effective per review, that's a **$75M–$300M annual wedge market** 🔴, before subscriptions.
- **The multiplier persona:** ~10K vCISO/MSSP/compliance-consulting firms 🟡 each review reports for many clients — one firm can be worth 50–500 reports/yr.
- **Why now:** (a) LLM cost/quality finally makes 150-page extraction reliable and cheap (<$1 COGS/report 🟡); (b) vendor-count-per-company keeps climbing; (c) auditors and regulators increasingly ask for *evidence* of vendor review, not just collection.

## 5. Competition

| Player | What they do | Why ZCC survives them |
|---|---|---|
| Vanta / Drata (VRM modules) | AI summary of vendor docs inside their platform | Serves only their own subscribers; bundled feature depth is shallow (no CUECs/severity grading 🟡); can't do $49 one-offs without cannibalizing ACV |
| Whistic / Conveyor / SafeBase | Questionnaire exchange & trust centers | Adjacent workflow (vendor-side sharing); doesn't analyze the auditor's findings |
| SecurityScorecard / UpGuard / Bitsight | Outside-in security ratings | Different signal entirely; complementary |
| ProcessUnity / Prevalent / Venminder | Enterprise TPRM suites | 6-figure, 6-month sales; ignores mid-market and consultants |
| DIY (ChatGPT/Claude + PDF) | Free-form summarization | No schema, no severity model, no CUECs, no audit trail, confidentiality nightmare on consumer tools; ZCC's structured output + trust posture is the product |

**Moat trajectory (honest version):** none today → accumulate (1) the largest labeled corpus of SOC 2 exceptions + accuracy benchmark, (2) vendor-report graph across customers, (3) trust/compliance posture (own SOC 2), (4) workflow lock-in via annual re-review cycles. Speed and focus are the actual strategy for year one.

## 6. Business model

| Tier | Price | What it includes | Target persona |
|---|---|---|---|
| Pay-per-report | **$49/report** 🟢 (in code) | One analysis + DOCX | First-touch; occasional reviewers |
| Starter | **$99/mo** 🔴 | 5 reports/mo, portfolio dashboard, expiry reminders | Lean security teams |
| Pro | **$399/mo** 🔴 | 25 reports/mo, autonomous outreach, API, multi-seat | GRC teams, vCISO firms |
| Enterprise | **$15–30K/yr** 🔴 | Volume, SSO, DPA/zero-retention, integrations | 500+ vendor programs |

- **Gross margin:** ≥95% 🟡 (LLM + storage COGS well under $1/report).
- **Expansion logic:** pay-per-report → 3rd purchase triggers "Starter pays for itself" prompt → portfolio + reminders create the annual renewal loop.
- **Pricing test planned:** $49 may be *too low* for the value (2–8 hrs of analyst time); test $79/$99 per report once accuracy proof exists. 🔴

## 7. Financial plan (12-month scenarios)

Assumptions: solo founder + contractors, ~$3–5K/mo total burn (infra <$500/mo at this scale 🟡), launch month 3.

| | **Bear** | **Base** | **Bull** |
|---|---|---|---|
| Month-12 one-off reports/mo | 30 | 120 | 350 |
| Month-12 subscribers (blended $180/mo 🔴) | 5 | 35 | 100 |
| **Exit MRR** | ~$2.4K | **~$12K** | ~$35K |
| Implied ARR run-rate | $29K | $144K | $420K |
| Cash need (12 mo, net) | ~$50K | ~$40K | ~$25K |

- **Base case logic:** GTM funnel (see [go-to-market-plan.md](go-to-market-plan.md)) delivers ~10K site visits/mo by month 12 at ~1.5% visitor→purchase 🔴; 20% of repeat purchasers convert to subscription 🔴.
- **Bear-case trigger:** if <100 total paid reports by month 6, the wedge hypothesis is wrong — diagnose (accuracy? trust? demand?) before spending on growth.
- **Burn multiple discipline:** stay under 2x (dollars burned per net-new ARR dollar) from first revenue onward.

## 8. Operating plan & milestones (seed-stage horizons: 3/6/12 months)

**Months 0–3 — Prove the product is trustworthy**
- Close the payment→report loop end-to-end; instrument everything (Sentry + PostHog).
- Golden-set benchmark: 15 real SOC 2 reports, human-verified; publish an accuracy number.
- Trust page live: retention/deletion policy, encryption, subprocessors.
- 10 design partners (5 vCISOs, 5 in-house GRC) using it free; 3 written testimonials.
- **Gate:** design partners say output is "usable without re-reading the PDF" ≥80% of the time. 🔴

**Months 3–6 — Prove someone will pay**
- Public launch (see GTM plan): Product Hunt, GRC communities, founder-led content.
- 100 cumulative paid reports; first 10 subscribers; $2.5K MRR.
- Ship source-linked findings + expiry reminders.
- **Gate:** ≥30% of purchasers buy a second report within 60 days (repeat-usage signal). 🔴

**Months 6–12 — Prove it compounds**
- $10K+ MRR; 5 vCISO/MSP partner firms on Pro; begin ZCC's own SOC 2 Type I.
- Ship autonomous outreach (the namesake feature) to Pro tier.
- **Decision gate at month 12:** raise seed (~$1–1.5M on the strength of $12K+ MRR growing >15% m/m 🔴) to pursue the platform + CAIA expansion, or continue bootstrapping profitably.

## 9. Team

- **Now:** solo technical founder 🟢 (repo history). Sufficient through month 6 with contractors for design and a fractional GRC advisor (critical: domain credibility for content + accuracy validation).
- **First hires (post-$10K MRR or post-seed):** (1) founding engineer (owns pipeline accuracy + integrations), (2) GRC-savvy growth/content lead. No salespeople until the Enterprise tier demonstrably pulls.

## 10. Funding strategy

Default: **bootstrap to the month-12 gate.** The wedge is cheap to run and the market is provable without capital. Raise only against evidence: repeat purchase rate, subscription conversion, and partner-channel pull. If raising, the story is "Stripe-simple wedge into the $8B TPRM stack, with a labeled-data moat compounding" — and the CAIA/AI-governance thesis becomes the expansion slide, not the company.

## 11. Top risks & mitigations

| Risk | Severity | Mitigation |
|---|---|---|
| NDA/confidentiality objections to uploading vendor reports | 🔴 Existential if ignored | Zero-retention default, DPA, delete-after-processing, own SOC 2 in year 1; address in messaging from day one |
| Platforms (Vanta/Drata) bundle "good enough" review | High | Depth (CUECs, severity, source links), serve non-platform buyers, integrate rather than compete |
| Accuracy failure destroys trust | High | Golden-set regression on every change; confidence scores; "analyst accelerant" positioning; source-page links |
| Single-founder execution risk | Medium | Ruthless scope (one document type until month 6); advisor bench |
| $49 anchors price too low | Medium | Price test at month 6; keep one-off as acquisition, make money on subscriptions |

## 12. KPI dashboard (reviewed monthly)

| Metric | Target |
|---|---|
| Paid reports/mo | 120 by month 12 |
| Visitor → purchase | ≥1.5% |
| Repeat purchase within 60 days | ≥30% |
| Purchaser → subscriber conversion | ≥20% of repeaters |
| Extraction accuracy vs. golden set | ≥95% on opinion/exceptions |
| Gross margin | ≥90% |
| MRR / growth | $12K / >15% m/m at month 12 |
| Runway | >12 months at all times |
