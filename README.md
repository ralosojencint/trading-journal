# Trading Journal SaaS

React + Vite + TypeScript + Tailwind frontend, a small Express server, Supabase Auth and PostgreSQL with Row Level Security on every table. It grows out of the single-file Trading Journal, which is kept in `legacy/`.

## Status (read first)
- Generated without network access: dependencies were **not installed and the project has not been built or run yet**. Run `npm install && npm run typecheck && npm run build` and fix anything reported before deploying.
- Needs your configuration: a Supabase project, the SQL migration, Auth URLs and Replit Secrets (see Setup).
- Included: landing page with Free vs Pro comparison and FAQ; sign up with email verification, log in, forgot and reset password, log out, protected dashboard; overview statistics; trading calendar with day report; add, edit and delete trades; history with search; CSV export as a server-side Pro-only endpoint.
- Not ported yet: analytics charts, goals, daily journal, risk limits, screenshot upload, multiple-account UI, PDF export, profile and settings pages. Their tables, RLS policies and the private screenshot bucket already exist in the migration.
- Payments are not implemented. Plans live in `subscriptions`; users can only read it, so only the server (service role) can change a plan.

## Setup
1. Create a project at supabase.com.
2. SQL Editor: paste and run `supabase/migrations/0001_init.sql`.
3. Authentication: enable the Email provider and turn on Confirm email. Under URL Configuration set the Site URL to your Replit URL and add `https://YOUR-URL/app` and `https://YOUR-URL/reset` as Redirect URLs.
4. Replit: upload this project and add Secrets `VITE_SUPABASE_URL`, `VITE_SUPABASE_ANON_KEY` and `SUPABASE_SERVICE_ROLE_KEY` (Supabase Settings > API). The service-role key is server-only: never prefix it with `VITE_`.
5. Run `npm install` once, then press Run (`npm run build && npm run start`). Publish with Replit Deployments.

Local: copy `.env.example` to `.env`, then `npm install`, `npm run build`, `npm run start` and open http://localhost:5000.

## Trying Pro
There is no checkout yet. In the Supabase SQL editor: `update public.subscriptions set plan_id = 'pro' where user_id = 'USER-UUID';`
