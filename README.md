# AkkoAudio (fresh deploy)

Music player + request-access gate + admin approve/deny + revocable tokens.

- Admin password never sent in plain text (challenge-response)
- Secret admin path + noindex
- New Supabase project friendly

## Quick setup

### 1. Supabase

1. Create a new project
2. SQL Editor → run all of `supabase.sql`
3. Settings → API → copy **Project URL** and **service_role** key

### 2. GitHub

1. New empty repo
2. Unzip this folder and push everything
3. Copy your old `music/`, `covers/`, `lyrics/` files into those folders if needed

### 3. Netlify

1. Import the GitHub repo
2. Publish directory: `.` (build command can be empty)
3. Environment variables:

| Name | Value |
|------|--------|
| `SUPABASE_URL` | Supabase project URL |
| `SUPABASE_SERVICE_ROLE_KEY` | service_role key |
| `ADMIN_PASSWORD` | your admin password |
| `SESSION_SECRET` | long random string (40+ chars) |

4. Deploy

### 4. URLs

- Site: `https://YOUR-SITE.netlify.app/`
- Admin: `https://YOUR-SITE.netlify.app/a/k7m2x9`

Change `k7m2x9` in `netlify.toml` to a private random slug, then redeploy. Bookmark it.

## Access flow

1. User requests access on the site
2. You approve in admin → copy token (shown once)
3. User pastes token → stored in their browser
4. Revoke in admin → access ends immediately

## Rotate secrets

If someone had an old password: set a new `ADMIN_PASSWORD` **and** new `SESSION_SECRET`, then redeploy.
