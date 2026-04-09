# Use loading.tsx for route-level loading states

**Impact:** MEDIUM | **Category:** quality | **Effort:** trivial

> Add loading.tsx to route segments with slow data fetching. It provides instant visual feedback during navigation.

## Why This Matters

Next.js wraps `page.tsx` in a Suspense boundary using `loading.tsx` as the fallback. This means:
- Navigation shows instant feedback
- The page shell renders immediately
- Slow data doesn't block the UI

## Good

```tsx
// app/(dashboard)/scans/loading.tsx
export default function Loading() {
  return <ScanListSkeleton />
}
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
