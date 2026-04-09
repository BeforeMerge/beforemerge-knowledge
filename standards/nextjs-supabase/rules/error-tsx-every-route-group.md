# Add error.tsx to every route group

**Impact:** HIGH | **Category:** quality | **Effort:** small

> Each route group ((auth), (dashboard), (content)) should have its own error boundary to contain failures.

## Why This Matters

Error boundaries contain failures:
- A bug in settings doesn't crash the dashboard
- A failed API call shows a retry button, not a white screen
- Users stay in the app instead of seeing a full-page error

## Required Files

```
app/(auth)/error.tsx
app/(dashboard)/error.tsx
app/(content)/error.tsx
app/(marketing)/error.tsx
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
