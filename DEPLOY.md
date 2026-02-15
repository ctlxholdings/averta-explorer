# Averta Explorer — Deployment Record

## Live URL

**https://averta.ctlx.holdings**

## What this is

Single-page interactive DD explorer for Averta solar portfolio.
Self-contained HTML — React + Recharts + Tailwind loaded from CDN, all data embedded.
No build step. No dependencies. No server.

## Files

```
deploy/
├── index.html      ← averta_explorer_v4.html renamed
├── vercel.json     ← Vercel config (no build, static)
└── DEPLOY.md       ← this file
```

## Infrastructure

| Layer | Detail |
|-------|--------|
| GitHub repo | https://github.com/ctlxholdings/averta-explorer |
| Vercel project | `deploy` (under ctlxs-projects-f4fd2bff) |
| Vercel default URL | deploy-sigma-livid.vercel.app |
| Custom domain | averta.ctlx.holdings |
| DNS | Squarespace — A record: `averta` → `76.76.21.21` |
| SSL | Auto-provisioned by Vercel |

## How it was deployed (2026-02-15)

### 1. Created GitHub repo

```bash
cd 01-Averta/01_model/frontend/deploy
git init
git add index.html vercel.json
git commit -m "Averta Explorer v4 — DD interactive model"
gh repo create ctlxholdings/averta-explorer --public --source=. --push
```

### 2. Deployed to Vercel

```bash
vercel --yes --prod
```

Vercel auto-linked to the GitHub repo. No build step needed — serves `index.html` as static.

### 3. Added custom domain

```bash
vercel domains add averta.ctlx.holdings
```

### 4. Configured DNS in Squarespace

In Squarespace → Domains → ctlx.holdings → DNS Settings:

| Type | Host | Data |
|------|------|------|
| A | `averta` | `76.76.21.21` |

Note: CNAME (`cname.vercel-dns.com`) was tried first but had SSL issues with Squarespace. A record to `76.76.21.21` works reliably — same pattern used for `learn.ctlx.holdings` and `risk.ctlx.holdings`.

## To update

Push changes to `main` on GitHub — Vercel auto-deploys on every push.

```bash
cd 01-Averta/01_model/frontend/deploy
git add -A && git commit -m "description of change" && git push
```

## Notes

- File size: ~170KB (well under Vercel limits)
- No API calls — everything is embedded JSON
- Works offline once loaded
- Mobile-responsive (Tailwind)
