# GuardCheck — TanStack Start App

QR-based attendance app for security guards built on TanStack Start (React 19 + TanStack Router + Vite 7), Tailwind v4, shadcn/ui, and Supabase.

## Stack

- **Frontend / SSR**: TanStack Start (`@tanstack/react-start`) + React 19
- **Build tool**: Vite 7 (wrapped by `@lovable.dev/vite-tanstack-config`)
- **UI**: Tailwind CSS v4, Radix UI, shadcn/ui components
- **Data**: `@tanstack/react-query`, Supabase (`@supabase/supabase-js`)
- **Forms / Validation**: react-hook-form + zod
- **Languages**: TypeScript

## Project Layout

- `src/routes/` — TanStack Router file-based routes (`__root.tsx`, `_app.*.tsx`, `login.tsx`, `signup.tsx`)
- `src/components/` — UI components (incl. shadcn/ui)
- `src/lib/` — utilities, auth context, Supabase client
- `src/integrations/` — third-party integrations
- `src/hooks/` — React hooks
- `supabase/` — Supabase migrations / config
- `vite.config.ts` — Vite config (wraps `@lovable.dev/vite-tanstack-config`)
- `wrangler.jsonc` / `netlify.toml` — original Cloudflare/Netlify deploy presets (not used on Replit)

## Replit Setup

- **Workflow**: `Start application` runs `npm run dev` on port `5000` (webview).
- **Vite dev server**: bound to `0.0.0.0:5000`, `allowedHosts: true` so the Replit iframe proxy can reach it.
- **Env vars**: stored in `.env` (Supabase URL + keys, Resend, etc.).
- **SSR**: disabled (`defaultSsr: false` in `src/router.tsx`). The Replit dev preview iframe injects a devtools script into the document head that conflicts with TanStack's SSR head output, causing React 19 hydration mismatches. Client-only rendering avoids this and matches how the app would behave in most production hosting setups for this stack.

## Scripts

- `npm run dev` — start Vite SSR dev server
- `npm run build` — production build (Cloudflare Workers preset via lovable config)
- `npm run preview` — preview built client
- `npm run lint` / `npm run format`

## Deployment

Configured as **autoscale** running `npm run dev`. The original project targets Cloudflare Workers / Netlify; on Replit the dev server is used because the build output is Workers-specific. Switch to a Node SSR build if you want a production-grade Replit deployment.
