# Use notFound() for invalid dynamic route params

**Impact:** MEDIUM | **Category:** quality | **Effort:** trivial

> When a dynamic route param doesn't match any record, call notFound() from next/navigation to show the 404 page.

## Why This Matters

`notFound()` triggers the nearest `not-found.tsx` page, giving users a clear 404 instead of a crash.

## Good

```typescript
import { notFound } from "next/navigation"

export default async function RulePage({ params }) {
  const rule = await getRule(params.slug)
  if (!rule) notFound()
  return <RuleDetail rule={rule} />
}
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
