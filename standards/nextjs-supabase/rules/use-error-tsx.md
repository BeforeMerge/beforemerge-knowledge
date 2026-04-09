# Use error.tsx for route-level error boundaries

**Impact:** HIGH | **Category:** quality | **Effort:** trivial

> Every route group should have an error.tsx to prevent crashes from propagating to the entire app.

## Why This Matters

A bug in `/settings` shouldn't crash `/dashboard`. Each route group needs its own error boundary.

## Good

```tsx
// app/(dashboard)/error.tsx
"use client"

export default function Error({
  error,
  reset,
}: {
  error: Error & { digest?: string }
  reset: () => void
}) {
  return (
    <div>
      <h2>Something went wrong</h2>
      <button onClick={() => reset()}>Try again</button>
    </div>
  )
}
```

**Note:** `error.tsx` must be a client component (`"use client"`).

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
