# Keep .env.example in sync with actual environment variables

**Impact:** HIGH | **Category:** quality | **Effort:** small

> Maintain a .env.example file with all required variables (no values). New developers can't set up the project without it.

## Why This Matters

`.env.example` is the contract for required environment variables.

## Good

```env
# .env.example — committed to git
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
GITHUB_APP_ID=
GITHUB_APP_PRIVATE_KEY=
ANTHROPIC_API_KEY=
```

## Audit

Regularly grep for `process.env.` and compare against `.env.example`.

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
