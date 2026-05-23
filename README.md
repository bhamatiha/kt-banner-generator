# KT Cloud Banner Generator

Cloud-first banner generator for KT/event promos.

## Deploy without a computer
1. Upload this ZIP to GitHub using GitHub mobile/browser.
2. Connect the repository to Netlify.
3. Build command: `npm run build`
4. Publish directory: `dist`

## Environment variables

### Required only if you use Supabase save/upload
- `VITE_SUPABASE_URL`
- `VITE_SUPABASE_ANON_KEY`

### Required only if you use AI theme generation
- `OPENAI_API_KEY`

## Supabase tables

Run this SQL in Supabase SQL Editor:

```sql
create table if not exists banners (
  id uuid primary key default gen_random_uuid(),
  created_at timestamptz default now(),
  name text,
  size text,
  sport text,
  template_key text,
  theme_json jsonb,
  data_json jsonb
);

alter table banners enable row level security;

create policy "Allow public read banners"
on banners for select
using (true);

create policy "Allow public insert banners"
on banners for insert
with check (true);
```

For production, replace public policies with proper login-based policies.
