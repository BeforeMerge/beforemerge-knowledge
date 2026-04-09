# Performance Optimization Checklist for Next.js

> Image optimization, font loading, dynamic imports, bundle analysis, Suspense streaming, and ISR patterns.

# Performance Optimization Checklist

## Images
- [ ] Use `next/image` for all images
- [ ] Set explicit `width` and `height` to prevent CLS
- [ ] Use `priority` for above-the-fold images
- [ ] Use `sizes` prop for responsive images

## Fonts
- [ ] Use `next/font` instead of Google Fonts CDN
- [ ] Preload critical fonts with `display: "swap"`

## Code Splitting
- [ ] Use `next/dynamic` for heavy client components
- [ ] Set `ssr: false` for browser-only libraries
- [ ] Analyze bundle with `@next/bundle-analyzer`

## Data Fetching
- [ ] Server Components for initial data (zero JS)
- [ ] `Promise.all` for parallel independent fetches
- [ ] Appropriate cache/revalidation per route
- [ ] SWR or React Query for client-side polling

## Rendering
- [ ] `loading.tsx` for instant navigation feedback
- [ ] `<Suspense>` for independent data regions
- [ ] Server Components by default
- [ ] `"use client"` pushed as low as possible

## Database
- [ ] Indexes on all foreign keys
- [ ] RLS policies use `(select auth.uid())`
- [ ] No N+1 queries — use `.select("*, relation(*)")`

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
