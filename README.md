# Monorepo (Vercel)

This monorepo contains three apps, each deployed as a separate Vercel project. Only apps whose code (or workspace dependencies) changed are built on each push.

## Apps

| App             | Path                  | Framework            |
|-----------------|-----------------------|----------------------|
| next-web        | `apps/next-web`       | Next.js (App Router) |
| next-docs       | `apps/next-docs`      | Next.js (App Router) |
| vite-dashboard  | `apps/vite-dashboard` | Vite + React         |

## Local development

- Install dependencies (from repo root): `npm install`
- Build all apps: `npm run build`
- Run a single app:
  - `cd apps/next-web && npm run dev`
  - `cd apps/next-docs && npm run dev`
  - `cd apps/vite-dashboard && npm run dev`

## Vercel deployment

1. **Create one Vercel project per app** from this repository (e.g. import the same Git repo three times, or use [Vercel CLI](https://vercel.com/docs/cli) `vercel link --repo`).

2. **Set Root Directory** for each project in **Settings → Build & Deployment**:
   - Project for next-web: `apps/next-web`
   - Project for next-docs: `apps/next-docs`
   - Project for vite-dashboard: `apps/vite-dashboard`

3. **Build settings**
   - Next.js apps: use defaults (Vercel auto-detects).
   - vite-dashboard: set **Build Command** to `npm run build` and **Output Directory** to `dist`.

4. **Conditional builds**  
   With the repo connected via **GitHub** and Root Directory set per project, Vercel will skip building a project when the commit does not change that app or its workspace dependencies. No extra “Ignored Build Step” is required.

The repo uses **npm workspaces** and a single root `package-lock.json`; the lockfile must remain at the repository root for this behavior.
