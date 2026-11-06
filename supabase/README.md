# Bible Tracker sync — backend setup (Supabase)

Reuses the shared `sync_rows` table (same project as Pulse is fine).

## One-time setup

1. Apply `schema.sql` in the SQL Editor (idempotent; widens the domain check).
2. Authentication → URL Configuration:
   - Site URL: `https://changelinglabs.com/bible-tracker/`
   - Redirect URLs: `https://changelinglabs.com/bible-tracker/` and `http://localhost:8901/`
3. Authentication → Email Templates → **Magic Link** (and **Confirm signup**):
   make sure the 6-digit code is visible, e.g. add
   `<p>Your sign-in code: <strong>{{ .Token }}</strong></p>`.
   The code is the primary sign-in method in the app because each installed
   Safari web app / home-screen app has its own storage and a magic link
   always opens in a browser, never inside the installed app.
4. Email provider stays on (default). Free tier is enough, but raise
   Authentication → Rate Limits → **Rate limit for sending emails** if you
   expect more than a couple of sign-ins per hour.

Publishable key ships in `app.js` (see `SYNC_CONFIG`). No secrets committed.