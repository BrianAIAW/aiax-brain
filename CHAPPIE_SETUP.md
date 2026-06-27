# 🤝 Chappie Setup — Sync the AIAX Brain into Obsidian

Instructions for Chappie (OpenClaw assistant) to connect the Base44 work record to the Obsidian brain via GitHub.

**Goal:** Keep a local Obsidian vault automatically in sync with the private GitHub repo `BrianAIAW/aiax-brain`. The Superagent commits journal + systems notes to this repo; Chappie pulls them into the vault so they appear in Obsidian.

---

## What you need
- The private repo: `https://github.com/BrianAIAW/aiax-brain`
- A **GitHub Personal Access Token (PAT)** with `repo` scope (private repo = auth required).
- Git installed on the machine running Obsidian.
- The path to the Obsidian vault folder (or a dedicated subfolder inside it).

---

## Step 1 — Get a GitHub token (one time)
1. Go to https://github.com/settings/tokens → **Generate new token (classic)**.
2. Scope: check **`repo`**.
3. Copy the token (starts with `ghp_…`). Store it securely.

## Step 2 — Clone the repo into the vault (one time)
```bash
cd "/path/to/your/ObsidianVault"
git clone https://github.com/BrianAIAW/aiax-brain.git AIAX-Brain
```
This creates an `AIAX-Brain/` folder inside the vault containing `index.md`, `JOURNAL/`, and `SYSTEMS/`. Obsidian will pick it up automatically.

When prompted for credentials: username = `BrianAIAW`, password = the **PAT** from Step 1.

## Step 3 — Keep it in sync (ongoing)
Have Chappie run this on a schedule (e.g. every 10–15 min, or on demand):
```bash
cd "/path/to/your/ObsidianVault/AIAX-Brain"
git pull --rebase
```
That single command brings in every new journal entry and systems update the Superagent has committed.

### Optional: two-way sync
If notes are ALSO edited inside Obsidian and should flow back to GitHub:
```bash
cd "/path/to/your/ObsidianVault/AIAX-Brain"
git add -A
git commit -m "Obsidian edits $(date +%F-%H:%M)"
git pull --rebase
git push
```

---

## Recommended: Obsidian Git plugin (simplest)
Instead of scripting, you can use the community plugin:
1. Obsidian → Settings → Community plugins → Browse → **Obsidian Git** → Install + Enable.
2. Set **Auto pull interval** to e.g. 10 minutes.
3. Point it at the `AIAX-Brain` folder / repo.
Chappie then only needs to ensure the token/credentials are configured once.

---

## How the workflow runs
1. Superagent does Base44 work (apps, billing, docs, audits).
2. Superagent commits a dated entry to `JOURNAL/` and updates `SYSTEMS/` in `aiax-brain`.
3. Chappie (or Obsidian Git) runs `git pull`.
4. The Obsidian brain updates automatically — graph view, backlinks, and search all work.

## Repo structure
```
aiax-brain/
├── index.md            # master map-of-content
├── CHAPPIE_SETUP.md    # this file
├── JOURNAL/            # dated daily logs (YYYY-MM-DD.md)
└── SYSTEMS/            # living reference docs
```

---
_Questions for the Superagent: if Chappie needs a different structure, folder names, or a webhook-style push instead of pull, just say so and it will adapt the repo._