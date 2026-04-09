# Use a lib/ directory for shared utilities

**Impact:** LOW | **Category:** architecture | **Effort:** trivial

> Centralize shared logic (auth, database clients, formatters) in a lib/ directory to avoid duplication.

## Why This Matters

A `lib/` directory creates a clear boundary between:
- **Route code** (`app/`) — page rendering and routing
- **Shared logic** (`lib/`) — auth, database, AI, integrations
- **Components** (`components/`) — reusable UI

## Recommended Structure

```
lib/
  supabase/
    server.ts      # createClient()
    admin.ts       # createAdminClient()
    client.ts      # browser client
  auth.ts          # requireAuth(), session helpers
  content-crud.ts  # generic CRUD factory
  ai/              # AI service layer
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
