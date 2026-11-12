# Deploy

1. Fork/copy this repo to GitHub account DailyWatchkw.
2. Supabase: create a free project, run supabase/schema.sql in SQL Editor, copy Project URL + service_role key (Settings > API). Never put the key in frontend code.
3. Render: New > Blueprint, select the repo. Fill SUPABASE_URL, SUPABASE_SERVICE_ROLE_KEY, PUBLIC_URL=https://muse.soitworks.online
4. GitHub repo Settings > Secrets and variables > Actions > Variables: KEEP_ALIVE_URL=https://muse.soitworks.online
5. Domain: Render service > Settings > Custom Domains > add muse.soitworks.online. In Cloudflare DNS for soitworks.online add CNAME muse -> <service>.onrender.com (DNS only / grey cloud first, until Render verifies, then as advised).
6. Verify: /health returns {"ok":true}, homepage loads, submit a test code, restart the Render service, confirm the code is still there (proves Supabase persistence).

Anti-sleep: server self-pings PUBLIC_URL/health every 10 min + GitHub Actions keep-alive every 10 min. Render free gives 750 instance-hours/month; one always-on service uses ~730h.
Images: uploads still live on the instance filesystem and are lost on restart. Move to Supabase Storage only if gallery persistence becomes a real need - not in v1, to keep it simple.
