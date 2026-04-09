# Never fetch the same data in both layout and page

**Impact:** MEDIUM | **Category:** performance | **Effort:** small

> Supabase client calls are NOT automatically deduplicated like fetch(). Querying the same data in layout.tsx and page.tsx doubles database load.

## Why This Matters

Next.js deduplicates `fetch()` calls during a render pass, but **Supabase client queries are NOT deduplicated**.

## Good

```typescript
// Fetch in layout, pass to page via context or props
// OR fetch only in page, not in layout
```

## Bad

```typescript
// layout.tsx
const { data: user } = await supabase.from("profile").select("*")

// page.tsx (same route)
const { data: user } = await supabase.from("profile").select("*")
// Same query runs TWICE!
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
