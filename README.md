# BraveEcom: AI Studio → GitHub → Vercel auto deploy

This repository is now configured so changes synced from **Google AI Studio** to GitHub can be automatically deployed to **Vercel production**.

## What was added

- GitHub Actions workflow: `.github/workflows/vercel-auto-deploy.yml`
- Trigger: every push to `main` or `master` (plus manual run with `workflow_dispatch`)
- Deployment path: Vercel CLI (`pull` → `build` → `deploy --prod`)

## One-time setup

In GitHub repository settings, add these **Actions secrets**:

- `VERCEL_TOKEN`
  - Create in Vercel: **Settings → Tokens**
- `VERCEL_ORG_ID`
  - From Vercel project `.vercel/project.json` or Vercel dashboard
- `VERCEL_PROJECT_ID`
  - From Vercel project `.vercel/project.json` or Vercel dashboard

> `vercel pull` writes `.vercel/project.json` and uses the org/project IDs.
> Keep `.vercel` out of git if it contains local-only metadata.

## How this works with Google AI Studio

1. Connect your AI Studio project to this GitHub repository.
2. Ensure AI Studio writes changes to `main` (or merge PRs into `main`).
3. Each push triggers the GitHub Action.
4. The workflow deploys the latest commit to Vercel production automatically.

## Optional hardening

- Require pull requests before merging to `main`.
- Add branch protection checks for this workflow.
- Add preview deployment workflow for non-main branches.
