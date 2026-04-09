# The Three Supabase Clients — When to Use Each

> Deep dive into createClient(), createAdminClient(), and createReadOnlyClient(). Decision tree for choosing the right client in Next.js.

# The Three Supabase Clients — When to Use Each

BeforeMerge (and any production Next.js + Supabase app) uses three distinct Supabase client types. Choosing the wrong one is either a security vulnerability or a broken feature.

## The Three Clients

### 1. createClient() — Authenticated, RLS-Enforced

**Use for:** Dashboard pages, user-facing queries, any component that should respect the logged-in user's permissions.

```typescript
import { createClient } from "@/lib/supabase/server"

export default async function DashboardPage() {
  const supabase = await createClient()
  const { data: scans } = await supabase.from("scans").select("*")
  // Only returns scans for the user's organization (RLS enforced)
}
```

**How it works:** Reads the user's session from cookies. PostgreSQL evaluates RLS policies using `auth.uid()` from the session JWT.

### 2. createAdminClient() — Service Role, Bypasses RLS

**Use for:** Server actions that write data, cron jobs, scanner callbacks, AI service calls — any backend operation that needs full access.

```typescript
import { createAdminClient } from "@/lib/supabase/admin"

export async function createScan(data: ScanInput) {
  const { orgId } = await requireAuth()  // Verify user first!
  const admin = createAdminClient()
  await admin.from("scans").insert({ ...data, organization_id: orgId })
}
```

**Warning:** This client bypasses ALL RLS policies. A missing `organization_id` filter returns data from all orgs.

### 3. createReadOnlyClient() — Anon Key, Public Data Only

**Use for:** Public pages (explore, content detail, marketing) where no user is logged in.

```typescript
import { createReadOnlyClient } from "@/lib/supabase/readonly"

export default async function ExplorePage() {
  const supabase = createReadOnlyClient()
  const { data } = await supabase
    .from("rules")
    .select("*")
    .eq("is_published", true)
    .eq("visibility", "public")
}
```

## Decision Tree

```
Is this a public page (no login required)?
  → Yes → createReadOnlyClient()
  → No  → Is this a read operation?
            → Yes → createClient() (RLS-enforced)
            → No  → Is this a write/mutation?
                     → Yes → createAdminClient() + requireAuth()
```

## Common Mistakes

1. **Using admin client for reads** — bypasses RLS, exposes all data
2. **Using authenticated client for public pages** — errors when no user is logged in
3. **Using admin client without requireAuth()** — any unauthenticated request can trigger writes
4. **Importing admin client in "use client" files** — leaks service_role key to browser

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
