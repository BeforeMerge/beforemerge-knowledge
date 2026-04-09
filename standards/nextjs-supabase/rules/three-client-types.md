# Use three distinct Supabase client types

**Impact:** CRITICAL | **Category:** security | **Effort:** medium

> Use createClient() for authenticated pages (RLS enforced), createAdminClient() for server-side writes (service_role), and createReadOnlyClient() for public pages (anon key).

## Why This Matters

Each client type has different security characteristics:

| Client | RLS | Use Case |
|--------|-----|----------|
| `createClient()` | Enforced | Dashboard pages, user-facing queries |
| `createAdminClient()` | **Bypassed** | Server actions for writes, cron jobs |
| `createReadOnlyClient()` | Enforced (anon) | Public pages (explore, content) |

## Good

```typescript
// Page component — RLS enforced
const supabase = await createClient()
const { data } = await supabase.from("scans").select("*")

// Server action — needs service_role for writes
const admin = createAdminClient()
await admin.from("scans").insert({ ... })
```

## Bad

```typescript
// Page component using admin client — bypasses RLS!
const admin = createAdminClient()
const { data } = await admin.from("scans").select("*") // sees ALL orgs!
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
