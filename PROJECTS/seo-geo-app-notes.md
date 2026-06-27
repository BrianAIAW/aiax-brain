# AIAW — How We Built SEO, GEO & the App (Build Notes + Learnings)

_Last updated: 2026-06-26_

This note documents how the SEO service, the GEO (AI Visibility) service, and the
in-app SEO Platform were set up for Ai Agent Worx — plus what we learned along the way.
It's a companion to the master playbook (`/.agents/skills/aiaw-knowledge/AIAW_PROJECT_MASTER.md`).

---

## 1. The App (AIAW SEO Platform)

- **Base44 app_id:** `6a3affa63ed9a93ed0f0ba39`
- **Project (client) record:** Ai Agent Worx — `6a3b00ca3ed9a93ed0f0baac`, domain `https://aiagentworx.ai`
- **Core backend functions:**
  - `runSiteAudit` — technical SEO crawl → Health Score + AuditIssue records
  - `runGeoAudit` — AI-visibility audit → GEO score + AuditIssue (category=GEO) records
  - `answerSeoQuestion` — in-app AI assistant (Claude Sonnet 4.6 / Opus) that teaches SEO + GEO and points users to the in-app tools
  - `generateReport` — client-facing PDF/HTML report (now includes a GEO section)
- **Learn section:** SEO topics + a dedicated GEO manual (Beginner/Intermediate/Advanced), AIAW plain-English voice
- **Models:** Claude Sonnet 4.6 + Opus for summaries/answers
- **Data integrity rule:** all reports/audits pull REAL data only — demo/seeded data was purged. Never show invented keywords, scores, or issues.

## 2. SEO Service Setup

- Technical audit (runSiteAudit) produces a Health Score (0–100) and concrete AuditIssue records.
- Report (generateReport) renders: Health Score tiles, executive summary (LLM, brand voice), keyword section (real GSC data or "connect Search Console" empty state), and now a GEO section.
- Integrations available: Gmail, Google Drive, Google Docs, Google Search Console, LinkedIn.
- Lead conversion automation is **email-based** — automated LinkedIn DM replies are NOT possible (platform API restriction). Assistant drafts LinkedIn replies for manual send.

## 3. GEO Service Setup (the new service)

GEO = Generative Engine Optimization = getting cited by AI answer engines (ChatGPT, Claude, Perplexity, Google AI Overviews).

**What `runGeoAudit` checks (9 checks):**
1. ChatGPT Search crawler (OAI-SearchBot) access
2. Claude web search (Claude-SearchBot) access
3. Perplexity (PerplexityBot) access
4. Structured Data (JSON-LD) present
5. **FAQ Schema (FAQPage)** — highest-impact content format
6. Question-based headings
7. Content depth (word count)
8. Clear contact / identity signals
9. About / authority page linked

**Rollout — GEO became the 9th service across ALL surfaces:**
- Website: dedicated `geo.html` (Service + FAQPage schema), `about.html` (AboutPage + Organization schema), homepage grid as Service 03 of 9, nav + footer + sitemap on all 12 pages.
- App: GEO Learn manual, GEO Audit module, GEO report section, assistant teaches GEO.
- Phone attendant: voice SERVICES_OVERVIEW + SMS services list updated to 9 services incl. GEO.
- Service Registry: `aiaw-knowledge/services.json` + `sync_check.py` verifier (validates 9 services across all 8 surfaces).

**Proof point (our own site):** aiagentworx.ai GEO audit went **78 → 89 → 100/100** (9/9 checks).
- 78→89: added About page + `/faq.html` with FAQPage schema
- 89→100: added FAQPage schema directly to the HOMEPAGE `<head>`

## 4. Pricing Status (as of 2026-06-26)

- **Only ONE service has a public fixed price:** AI Phone Receptionist = **$497 setup + $97/mo** (shown on FAQ).
- **All other services (SEO, GEO, websites, automation) are quote-based** — "tailored after a free discovery call."
- **GEO has NO fixed price yet.** Positioned as standalone OR an add-on to any SEO plan.
- **Suggested GEO pricing (DRAFT — awaiting Brian's confirmation, not published):**
  - GEO Audit (one-time): ~$297
  - GEO add-on to SEO: ~+$150/mo
  - GEO standalone: ~$497 setup + ~$197/mo
- **Open decision:** does AIAW want a PUBLIC price page, or stay quote-based? (Currently quote-based except receptionist.)

---

## 5. Key Learnings

1. **Schema must live on the HOMEPAGE, not just subpages.** The GEO audit checks the root URL. FAQPage schema on `/faq.html` alone did NOT clear the FAQ check — we had to embed it in `index.html <head>`. Same applies to any schema you want credited.
2. **When adding a page, link it site-wide.** A new page (About, GEO, FAQ) must be linked in nav/footer on EVERY page, not just index. Verify with a per-page grep loop.
3. **One service = touch every surface.** Adding GEO meant updating website (12 pages), app (Learn/Audit/Report/Assistant), phone attendant (voice+SMS), registry, sitemap, docs. The `services.json` + `sync_check.py` system exists to prevent drift — run it after every service change.
4. **Never invent data or prices.** Reports show only real audit data; pricing stays "tailored" until Brian gives real numbers. One fabricated number erodes trust.
5. **GEO doubles as its own sales demo.** "We took our own site from 78 to 100 — here's the audit" is the strongest pitch for selling GEO. Practice what we preach.
6. **Cache lag on deploy.** Cloudflare Pages takes ~1–2 min to propagate; always re-verify live with a cache-busting `?v=timestamp` before declaring done.
7. **Some automations are platform-blocked.** Automated LinkedIn DMs aren't possible — pivot to email-based lead conversion + assistant-drafted manual replies.
