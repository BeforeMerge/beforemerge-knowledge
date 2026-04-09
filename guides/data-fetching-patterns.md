# Data Fetching Patterns in Next.js + Supabase

> Comparison of data fetching approaches: server component fetching, SWR, React Query, and Supabase real-time subscriptions.

# Data Fetching Patterns

## Pattern 1: Server Component Fetch (Default)

Best for: Page data, initial load, SEO-critical content.

```tsx
export default async function RulesPage() {
  const supabase = await createClient()
  const { data: rules } = await supabase.from("rules").select("*")
  return <RuleList rules={rules} />
}
```

## Pattern 2: SWR / React Query (Client-Side)

Best for: Real-time updates, optimistic UI, data that changes frequently.

```tsx
"use client"
import useSWR from "swr"

export function NotificationBell() {
  const { data } = useSWR("/api/notifications", fetcher, {
    refreshInterval: 30000,
  })
}
```

## Pattern 3: Supabase Real-Time

Best for: Collaborative features, live dashboards.

```tsx
"use client"
const channel = supabase
  .channel("scans")
  .on("postgres_changes", { event: "UPDATE", schema: "public", table: "scans" },
    (payload) => updateScanStatus(payload.new)
  )
  .subscribe()
```

## Decision Matrix

| Need | Pattern | Why |
|------|---------|-----|
| Page data | Server Component | Zero JS, fastest |
| Form state | Server Action | No API route needed |
| Polling/refresh | SWR | Built-in revalidation |
| Live updates | Supabase Realtime | Push, not poll |
| Complex cache | React Query | Fine-grained control |

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
