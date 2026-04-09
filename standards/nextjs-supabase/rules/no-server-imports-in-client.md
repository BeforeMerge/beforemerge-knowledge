# Never import server-only code in client components

**Impact:** CRITICAL | **Category:** security | **Effort:** medium

> Files with "use client" must never import server-only modules like database clients, API keys, or service role credentials.

## Why This Matters

Next.js bundles all imports in `"use client"` files for the browser. If you import a database client, the connection string ends up in the client bundle — visible to anyone with browser DevTools.

## Good

```typescript
// lib/supabase/admin.ts
import "server-only"  // Prevents accidental client import
import { createClient } from "@supabase/supabase-js"

export const adminClient = createClient(
  process.env.SUPABASE_URL!,
  process.env.SUPABASE_SERVICE_ROLE_KEY!
)
```

## Bad

```typescript
// components/dashboard.tsx
"use client"
import { adminClient } from "@/lib/supabase/admin"  // LEAKED!
```

## How to Fix

1. Add `import "server-only"` to all server-only modules
2. Next.js will throw a build error if a client component tries to import it

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
