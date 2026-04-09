# Store sensitive env vars without NEXT_PUBLIC_ prefix

**Impact:** CRITICAL | **Category:** security | **Effort:** trivial

> Only the Supabase URL and anon key should have NEXT_PUBLIC_ prefix. All other Supabase credentials are server-only.

## Why This Matters

`NEXT_PUBLIC_` variables are **inlined into the client bundle** at build time. Anyone can see them in the browser.

## Safe to Make Public

```env
NEXT_PUBLIC_SUPABASE_URL=https://xxx.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJ...  # anon key is safe — RLS protects data
```

## Must Stay Server-Only

```env
SUPABASE_SERVICE_ROLE_KEY=eyJ...
SUPABASE_DB_URL=postgresql://...
GITHUB_APP_PRIVATE_KEY=...
ANTHROPIC_API_KEY=sk-...
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
