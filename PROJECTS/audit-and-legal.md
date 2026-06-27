# AIAW Full System Audit + Legal Research — 2026-06-26

Comprehensive audit of everything built so far (website, app, phone attendant) BEFORE
building the customer portal. Plus legal research for an AI services business.

---

## PART 1 — AUDIT FINDINGS

### ✅ Website (12 pages) — HEALTHY
- Every page has: meta description, canonical, Open Graph, JSON-LD schema, exactly 1 H1, alt text on all images.
- Canonicals are extension-less (`/about`) and resolve 200 (Cloudflare strips `.html`). ✓ correct.
- About + GEO + FAQ linked in nav/footer across all 12 pages.
- GEO audit on own site = **100/100** (9/9 checks).

### ✅ Phone Attendant — HEALTHY
- Live endpoint returns HTTP 200.
- XML escaping correct (no raw `&` in TwiML URLs).
- 16 try/catch blocks, no hardcoded secrets, `<Gather>` logic present (12 gathers).
- Says "nine main services" — in sync.

### ✅ App (AIAW SEO Platform) — HEALTHY
- 4 backend functions: runSiteAudit, runGeoAudit, answerSeoQuestion, generateReport.
- Data is REAL (live audit results, no fake seeds). Data-integrity rule holding.
- All 8 surfaces in sync (sync_check.py passes).

### 🚨 GAPS / FIXES BEFORE PORTAL

| # | Severity | Finding | Fix |
|---|----------|---------|-----|
| 1 | **HIGH** | NO legal pages exist (no Privacy Policy, no Terms of Service) | Build both (see Part 2) — required before login/payments |
| 2 | HIGH | No AI-interaction disclosure anywhere (EU AI Act Art. 50, FTC) | Add "you're interacting with AI" notice to phone attendant + chat/assistant |
| 3 | MED | No cookie/privacy notice on website | Add privacy link in footer + basic cookie notice |
| 4 | MED | Footer has no Privacy/Terms links on any page | Add once legal pages exist |
| 5 | LOW | Phone attendant could log a call-recording/AI disclosure line | Add "calls handled by an AI assistant" disclosure |
| 6 | LOW | No favicon verified across pages | Quick check/add |

---

## PART 2 — LEGAL RESEARCH (AI Services Business)

Sources: toslawyer.com (AI ToS 2026), danielrosslawfirm.com (AI liability), CA OAG (CCPA),
lumalexlaw / Mayer Brown (AI SaaS contracting). **NOT legal advice — get an attorney to review final docs.**

### Why this matters for AIAW specifically
AIAW: (a) runs AI that produces outputs customers act on (audits, content, phone answers),
(b) collects personal data (leads, customer accounts), (c) will take recurring payments, and
(d) uses third-party AI (Anthropic/OpenAI/Google). All four trigger legal obligations.

### A. TERMS OF SERVICE — must include (7 pillars from 2026 AI ToS guidance):
1. **Define what the AI does** — plain, functional description (not marketing). "AIAW uses AI language models to generate SEO/GEO audits, draft content, and answer phone calls. Outputs are machine-generated and require human review."
2. **AI output ownership** — customer owns deliverables; AIAW retains license to operate/improve service; note similar outputs may be generated for others (no false exclusivity).
3. **Data usage & training** — state whether customer data trains models (recommended: NO training on customer data, or opt-out), how data is handled at subscription end.
4. **Limitation of liability for AI outputs** — AI outputs not guaranteed accurate/complete; customer must review/verify before acting; AIAW not liable for decisions made on unverified AI output; liability cap (commonly fees paid in last 12 months).
5. **Acceptable Use Policy** — prohibit illegal content, third-party data without consent, using outputs in regulated contexts without professional review, reverse-engineering.
6. **Right to modify terms** — 30-day notice for material changes via email; adapt to regulation.
7. **Disclose third-party AI providers** — Anthropic/OpenAI/Google may process inputs; their terms also apply.

Plus standard SaaS clauses: payment/billing/auto-renewal terms, cancellation/refund policy,
termination, warranty disclaimer ("as is"), indemnification, governing law (Nevada), dispute resolution.

### B. PRIVACY POLICY — must include (CCPA/CPRA + 20+ state laws + GDPR if EU):
- What personal data is collected (name, email, phone, payment, site/usage data).
- Why / how it's used; legal basis.
- Whether data is shared with third parties (Stripe, AI providers, Google) and why.
- Whether data trains AI (state clearly).
- Consumer rights: access, deletion, opt-out of sale/sharing, correction (CCPA).
- Data retention + security measures.
- Contact for privacy requests.
- Cookie usage.
- **CCPA threshold note:** full CCPA applies at ~$25M revenue OR 100k consumers OR 50%+ revenue from selling data — AIAW likely under thresholds NOW, but a compliant policy is best practice and future-proofs as you scale.

### C. AI-SPECIFIC DISCLOSURES (EU AI Act Art. 50 + FTC):
- **Disclose AI interaction up front** — phone attendant should say it's an AI assistant; chat/portal assistant should label itself AI.
- **FTC:** don't overstate what the AI can do (no deceptive claims); implement reasonable safeguards against foreseeable misuse.

### D. PORTAL-SPECIFIC (for the next phase):
- **Clickwrap consent** — customers must affirmatively accept ToS + Privacy Policy at signup (checkbox + timestamp logged).
- **Subscription/auto-renewal disclosure** — clear recurring-billing terms, cancellation method, before charging (FTC "click to cancel" + state auto-renewal laws).
- **Payment data** — never store raw card data; use Stripe (PCI handled by Stripe).
- **DPA** — if serving business customers, a Data Processing Addendum may be requested.

### Recommended deliverables
1. `privacy.html` — Privacy Policy page
2. `terms.html` — Terms of Service page
3. AI disclosure line in phone attendant + portal assistant
4. Footer Privacy/Terms links sitewide
5. Clickwrap consent at portal signup (next phase)
6. **Attorney review** before relying on these for protection.

> ⚠️ These are well-researched starting templates for AIAW's protection, NOT a substitute for a licensed attorney. Recommend a Nevada business/tech attorney review before launch.
