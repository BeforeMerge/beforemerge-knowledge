# Colocate page files with their route segment

**Impact:** MEDIUM | **Category:** architecture | **Effort:** small

> Keep page.tsx, layout.tsx, loading.tsx, and error.tsx together in the same route segment directory.

## Why This Matters

Colocating route files keeps related logic together:
- `page.tsx` — the route component
- `loading.tsx` — loading UI (automatic Suspense boundary)
- `error.tsx` — error boundary
- `layout.tsx` — shared layout

## Good

```
app/(content)/rules/[slug]/
  page.tsx
  loading.tsx
  error.tsx
```

## Bad

```
app/(content)/rules/[slug]/page.tsx
components/rules/RuleLoading.tsx   # loading state far from page
utils/rules/fetchRule.ts           # data fetching far from page
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
