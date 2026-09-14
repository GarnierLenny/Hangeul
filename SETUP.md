# Hangeul Blocks — backend setup

Single-file web game (`index.html`). Accounts + progress sync are **optional** —
the game plays fully without signing in; sign-in just saves/syncs progress.

## Supabase project

- Project: **Hangeul-Blocks** (`irdgjxbftfogqpdfdpdl`, region eu-west-2)
- API URL: `https://irdgjxbftfogqpdfdpdl.supabase.co`
- Publishable key (safe to ship in the client): `sb_publishable_L6As4b_DHRjOLvXp_Dj2Yw_Rhzl_hvC`
- These two values live in `index.html` (`SB_URL`, `SB_KEY`). Never put the **service_role**
  or **secret** key in the client.

## Database

Table `public.progress` with Row Level Security — each user reads/writes only their own row:

```
progress ( user_id uuid pk → auth.users, data jsonb, updated_at timestamptz )
```

Progress (`done` / `srs` stars / `streak`) is stored as JSON in `data`. On login the client
merges cloud + local, keeping the better of each, then pushes back up.

## Auth providers

### Email + password
Works out of the box. Note: **email confirmation is currently ON**, so a new signup must
click a confirmation email before signing in. To make testing frictionless, turn it off:
Supabase → Authentication → Sign-ups → **Confirm email** (off). Keep it on for production.

### Google (OAuth)
Google Cloud OAuth client + Supabase provider are configured and verified working.
The one fixed value Google needs, the Supabase **callback URL**:

```
https://irdgjxbftfogqpdfdpdl.supabase.co/auth/v1/callback
```

(Set as an Authorized redirect URI on the Google Cloud OAuth client.)

## Redirect URLs (important)

After Google signs a user in, the browser returns to the **app** URL. That URL must be in
Supabase → Authentication → **URL Configuration → Redirect URLs**. Add each place the app runs:

```
http://localhost:8123/index.html      # local testing
https://<your-deployed-url>/...        # production, once hosted
```

Also set **Site URL** to the main app URL. The client sends `redirectTo = <origin><pathname>`.

## Email delivery

Supabase's default email sender is rate-limited and testing-grade. For production
(confirmation + password-reset emails), configure custom SMTP.
