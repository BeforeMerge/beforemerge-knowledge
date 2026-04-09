# Use SWR or React Query for client-side real-time data

**Impact:** MEDIUM | **Category:** architecture | **Effort:** medium

> For data that changes frequently (notifications, dashboards), use SWR or React Query instead of manual useEffect + fetch.

## Why This Matters

SWR and React Query provide:
- **Automatic caching** and deduplication
- **Revalidation** on focus, interval, or mutation
- **Optimistic updates** for instant UI feedback
- **Error retry** with exponential backoff

## Good

```tsx
"use client"
import useSWR from "swr"

const fetcher = (url: string) => fetch(url).then(r => r.json())

export function NotificationBell() {
  const { data, error, isLoading } = useSWR("/api/notifications", fetcher, {
    refreshInterval: 30000,
  })
  // ...
}
```

## Bad

```tsx
"use client"
export function NotificationBell() {
  const [data, setData] = useState(null)
  const [loading, setLoading] = useState(true)
  useEffect(() => {
    const interval = setInterval(() => {
      fetch("/api/notifications")
        .then(r => r.json())
        .then(setData)
        .finally(() => setLoading(false))
    }, 30000)
    return () => clearInterval(interval)
  }, [])
}
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
