# Mark server modules with import "server-only"

**Impact:** HIGH | **Category:** security | **Effort:** trivial

> Add import "server-only" to any module that uses secrets, database connections, or server-only APIs.

## Why This Matters

The `server-only` package is a build-time safeguard. When imported, any attempt to bundle this module for the client will throw a build error.

## Good

```typescript
// lib/supabase/admin.ts
import "server-only"

export function createAdminClient() {
  return createClient(url, process.env.SUPABASE_SERVICE_ROLE_KEY!)
}
```

## How to Install

```bash
npm install server-only
```

Add `import "server-only"` as the first line of any file that:
- Uses `SUPABASE_SERVICE_ROLE_KEY`
- Accesses database directly
- Reads non-`NEXT_PUBLIC_` env vars

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
