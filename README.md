# Line Item Modeler (LIM) — UX Prototype

Gated UX review site for the OneStream **Line Item Modeler** prototype, using the
shared OneStream prototype chrome (OneStream Sans, brand-blue tiles, Vercel edge
auth gate). Source design: **People Planning (PLN)** in Figma.

## Structure

| File | Purpose |
|------|---------|
| `login.html` | Branded password login screen. |
| `portal.html` | UX Review portal — launcher tiles (Figma + HTML prototype). Lands here after login. |
| `index.html` | Root `/` — placeholder review frame ("coming soon"); becomes the HTML prototype/review frame later. |
| `middleware.js` | Vercel Edge Middleware — server-side gate. Cookie `lim_auth`. |
| `api/login.js`, `api/logout.js` | Edge auth functions. |
| `api/notes.js` | Shared UX-notes store (for the review frame, added later). |
| `vercel.json` | `no-store` caching for HTML/assets. |
| `fonts/`, `brandmark.svg`, `logo.png` | Shared OneStream brand assets. |

## Deploy

GitHub `akahan796/LIM` → Vercel (every push to `main` auto-deploys). Git author
must be `akahan@onestreamsoftware.com`.

### Required Vercel env vars (Project → Settings → Environment Variables)

- `ACCESS_PASSWORD` — reviewer login password.
- `SESSION_TOKEN` — long random secret (`openssl rand -hex 32`).

Until **both** are set the middleware fails open (site is public). Optional
`EDITOR_PASSWORD` / `EDIT_TOKEN` + a KV/Upstash store enable editable shared UX
notes once the review frame exists.

> After connecting the repo in Vercel, update the Line Item Modeler tile URL in
> the master `PORTAL/portal.html` with the assigned Vercel domain.

## Local preview

```
python3 serve.py   # http://localhost:4602  (auth/edge functions don't run locally)
```
