# aiagentworx.ai — How to Deploy the Public Website ⭐

**The public marketing site lives HERE in the Superagent workspace** at
`/app/website/*.html` (12 pages). It is NOT a separate Base44 app and NOT
the "AIAW SEO Platform" builder (that app is the internal SEO dashboard).

## Host
Cloudflare Pages — project name **`aiagentworx-site`**,
account_id **`51c3168cf8211c2c0668ab79f3e956c5`**
(source: `website/.wrangler/cache/pages.json`).

## Deploy command (verified live Jun 26, 2026)
```bash
cd /app/website && \
CLOUDFLARE_API_TOKEN="$CLOUDFLARE_PAGES_TOKEN" \
CLOUDFLARE_ACCOUNT_ID="51c3168cf8211c2c0668ab79f3e956c5" \
npx wrangler pages deploy . --project-name=aiagentworx-site --branch=main --commit-dirty=true
```

## Gotchas
- Use **`$CLOUDFLARE_PAGES_TOKEN`**, NOT `$CLOUDFLARE_API_TOKEN` (the latter
  authenticates to the wrong account `135ff8...` and fails).
- Must override `CLOUDFLARE_ACCOUNT_ID` to the config value above.
- `wrangler` runs via `npx` (auto-installs).

## Workflow to update the website
1. Edit the `/app/website/*.html` files directly myself.
2. Run `python3 /app/.agents/skills/aiaw-knowledge/sync_check.py` to verify
   all services are in sync across surfaces.
3. Run the deploy command above.
4. Live in 1–2 min at https://aiagentworx.ai (Cloudflare cache refresh).

**No builder bot needed for the website.** I edit + deploy it myself.
