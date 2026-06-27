# 🤝 Chappie Setup — Sync the AIAX Brain into Obsidian

**This repo is PUBLIC. No GitHub token / PAT is required.** Do not paste any `ghp_…` token anywhere — itʼs unnecessary.

**Goal:** Keep a local Obsidian vault in sync with the public GitHub repo `BrianAIAW/aiax-brain`. The Superagent commits journal + systems notes here; Chappie pulls them into the vault.

---

## Step 1 — Clone into the vault (one time, NO auth needed)
```bash
cd "/path/to/your/ObsidianVault"
git clone https://github.com/BrianAIAW/aiax-brain.git AIAX-Brain
```

## Step 2 — Keep it in sync (ongoing)
Run on a schedule (every 10–15 min) or on demand:
```bash
cd "/path/to/your/ObsidianVault/AIAX-Brain"
git pull --rebase
```

### Optional: Obsidian Git plugin (simplest)
1. Obsidian → Settings → Community plugins → Browse → **Obsidian Git** → Install + Enable.
2. Set **Auto pull interval** to ~10 minutes.
3. Point it at the `AIAX-Brain` folder.

---

## ⚠️ Security rule (because this repo is public)
This repo holds ONLY notes — journal, systems reference, project records.
**NEVER commit:** API keys, tokens, Stripe secrets, passwords, or raw customer PII.
Anything sensitive stays in the secure secret store / 1Password — never in this repo.

## Repo structure
```
aiax-brain/
├── index.md            # master map-of-content
├── CHAPPIE_SETUP.md    # this file
├── JOURNAL/            # dated daily logs (YYYY-MM-DD.md)
├── SYSTEMS/            # living reference docs
└── PROJECTS/           # deeper build/audit records
```

## How the workflow runs
1. Superagent does Base44 work.
2. Superagent commits a dated `JOURNAL/` entry + updates `SYSTEMS/`.
3. Chappie (or Obsidian Git) runs `git pull`.
4. The Obsidian brain updates automatically.