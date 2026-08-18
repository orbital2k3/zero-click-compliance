# ZCC Project Review

**Date:** 2026-08-18
**Scope:** Full repository review — product, code, and strategy documents — as the foundation for the [business plan](business-plan.md) and [go-to-market plan](go-to-market-plan.md).

Findings are tagged: 🟢 verified in the repo · 🟡 industry estimate · 🔴 assumption to validate.

---

## 1. Bottom line

**ZCC is a real, mostly-built MVP with a sharp wedge and a genuinely good recent pivot — but the repo contains two competing startup ideas, and the company needs to commit to one.**

What exists today is an AI-powered SOC 2 report analyzer: upload a vendor's SOC 2 Type II PDF, pay $49, and receive a structured risk analysis (auditor opinion, exceptions with severity grades, CUECs, subservice organizations) as a generated DOCX report. The original "autonomous outreach" vision (agent emails the vendor, intercepts the reply, parses the attachment) is scaffolded but not the current center of gravity — the May 2026 pay-per-report pivot is.

That pivot is the right call. It converts a hard enterprise-platform sale into a $49 credit-card transaction with near-zero adoption friction, and it creates a natural expansion path back to the platform vision.

---

## 2. What the product actually is (current state)

🟢 Verified by reading the code:

| Layer | Status | Evidence |
|---|---|---|
| React 19 + Vite frontend | Built | `zcc-web/` — landing, signup/login (Supabase Auth), upload with drag-and-drop, dashboard, report viewer (~2,100 LOC) |
| Express 5 + TypeScript API | Built | `zcc-api/` — reports, vendors, stripe, webhooks routes (~2,200 LOC) |
| Payments | Built (Stripe Checkout, $49/report, refund helper exists) | `routes/stripe.ts`, `lib/stripe.ts`, `lib/stripeRefund.ts` |
| PDF → structured analysis | Built, model-agnostic | `services/aiAnalyzer.ts` — Zod-validated JSON schema covering opinion, exceptions w/ risk levels, CUECs, subservice orgs |
| Report generation | Built | `services/docxGenerator.ts` (496 LOC — the largest service) |
| Async processing | Built | `worker/queue.ts` + `worker/processReport.ts` |
| Email (outreach vision) | Built but secondary | `services/emailService.ts` (Resend) |
| Database | Supabase Postgres w/ RLS, 3 migrations | `supabase/migrations/` |

**The domain modeling is the standout asset.** The `AIResponseSchema` in `aiAnalyzer.ts` shows real understanding of SOC 2 mechanics — it captures auditor opinion types (unqualified/qualified/adverse/disclaimer), carve-out vs. inclusive subservice methods, exceptions with vendor responses, and Complementary User Entity Controls. Most "AI document summary" competitors don't model CUECs at all, and CUECs are exactly what a GRC analyst needs to act on. This is the difference between a demo and a tool.

## 3. Technical gaps

1. **Zero tests.** 🟢 No test files exist anywhere in the repo. For a product whose entire value proposition is *accuracy of analysis*, this is the most important gap — you need a golden-set regression suite of real SOC 2 reports with known exceptions before you can claim reliability to a customer. (There is an untested-checklist in `TASK_2A_SUMMARY.md` acknowledging this.)
2. **The payment loop may not be closed end-to-end.** 🟡 Task 2A (upload) is documented complete; Stripe routes and webhook handlers exist, but there's no evidence of an end-to-end verified run (no tests, no E2E script). Before launch, run the full journey: signup → upload → pay → worker processes → DOCX delivered.
3. **No observability.** No error tracking (Sentry), no analytics, no funnel instrumentation. You can't run a PLG motion blind.
4. **Trust infrastructure is absent.** Customers will upload *confidential third-party audit reports*. There is no data-retention policy, no encryption-at-rest statement, no "we delete your PDF after N days" commitment, and ZCC itself has no SOC 2. This is the single biggest commercial blocker (see §5).
5. **Housekeeping:** a stale `.claude/worktrees/` copy of the repo is checked in; `SOC2_Review_Summary.docx` and `gemini-chat-050826.txt` are artifacts that should move out of the root. Secrets hygiene is good — only `.env.example` files are tracked. 🟢

## 4. The strategic fork in the repo

The repo contains **two different companies**:

| | **A: ZCC (SOC 2 vendor risk)** | **B: AI Governance Platform (CAIA/NAIC)** |
|---|---|---|
| Source docs | `zcc_implementation_plan.md`, `memory-bank/`, pay-per-report specs | `us_fin_ins_ai_governance_plan.md`, `competition_analysis.md` |
| Build status | ~4,400 LOC, working MVP | Zero code |
| Buyer | CISO / GRC analyst / vCISO, any industry | Chief Compliance Officer at insurance carriers |
| Sales motion | $49 self-serve → subscription | Enterprise, long-cycle, regulated |
| Timing bet | Evergreen pain (SOC 2 review is a decade-old chore) | Colorado AI Act effective 2026; "safe harbor" wedge |

**Recommendation: commit to A now; park B as a documented expansion thesis.** Reasons:

- A is built; B restarts from zero against funded competitors (ValidMind, FairNow, Credo AI — per your own `competition_analysis.md`).
- B's buyer (insurance compliance) is one of the slowest-buying personas in B2B; you'd need 12–18 months of runway before first revenue. 🟡
- A and B are not entirely disconnected: both sell to compliance/risk officers, and A's "third-party AI vendor oversight" is literally Phase 3 of the B plan. Winning A gives you the customer list and credibility to expand toward B later.
- The CAIA safe-harbor insight is genuinely clever — keep `competition_analysis.md` as a future-expansion memo, and revisit after ZCC reaches ~$25K MRR or if a design partner in insurance pulls you there. 🔴

## 5. The three business risks that matter most

1. **Confidentiality/NDA risk (existential if unaddressed).** SOC 2 reports are almost always distributed under NDA. Customers uploading a vendor's report to a third-party AI service may technically breach that NDA, and vendors may object. Mitigations: zero-retention processing option, delete-after-processing default, clear DPA, BYO-key/VPC tier later, and — critically — get ZCC's own SOC 2 Type I within the first year. This must be addressed in messaging from day one, not discovered by customers. 🔴 *validate with 5 design-partner conversations*
2. **Feature-not-a-company risk.** Vanta, Drata, SecurityScorecard, Whistic, and Conveyor all have or are building AI review of vendor security documents inside their platforms. 🟡 ZCC's defenses: (a) serve the huge population that does *not* live in those platforms (mid-market, vCISOs, consultants), (b) be the best-in-class depth play (CUECs, exception severity, cross-report vendor history) rather than a checkbox feature, (c) stay motion-incompatible — platforms can't easily do $49 anonymous-ish one-off transactions without cannibalizing their ACV.
3. **Accuracy liability.** If ZCC says "0 critical exceptions" and a customer relies on it and gets burned, the brand is dead. Mitigations: always link findings to source pages, show extraction confidence, position as "analyst accelerant" not "auditor replacement," and maintain the golden-set benchmark (see §3.1) with a published accuracy number.

## 6. What's genuinely strong

- **Wedge economics.** A GRC analyst spends 2–8 hours per SOC 2 review 🟡; at any loaded salary that's $150–$800 of labor. $49 for a 10-minute structured result is a trivially easy expense decision — often below corporate card approval thresholds.
- **The pivot discipline.** Moving from "autonomous agent platform" (hard to trust, hard to sell) to "pay-per-report" (instant value, self-serve) while keeping the agentic outreach as a *later* subscription feature is exactly the right sequencing.
- **Model-agnostic AI layer.** `aiAnalyzer.ts` takes any endpoint — no vendor lock-in, easy cost optimization as model prices fall.
- **Clean unit economics.** COGS per report ≈ LLM tokens for a 150-page PDF + storage ≈ well under $1 🟡 → 95%+ gross margin at $49.

## 7. Priority actions (pre-launch)

1. Close and verify the full payment→report loop end-to-end (finish Task 2B if incomplete).
2. Build the golden-set: 10–15 real SOC 2 reports with human-verified exception lists; measure and track extraction accuracy on every prompt/model change.
3. Write and publish the trust page: retention policy, deletion guarantees, encryption, subprocessor list.
4. Add Sentry + product analytics (PostHog or similar) before any traffic arrives.
5. Recruit 5–10 design partners (vCISOs and mid-market GRC leads) for free reports in exchange for accuracy feedback and testimonials.
6. Repo hygiene: remove the stale worktree copy and stray root artifacts; add a basic CI that at least type-checks both packages.

---

*Companion documents: [business-plan.md](business-plan.md) · [go-to-market-plan.md](go-to-market-plan.md)*
