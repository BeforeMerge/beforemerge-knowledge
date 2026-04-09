# Error Handling Architecture for Next.js + Supabase

> Error boundary hierarchy, structured logging with pino, user-friendly error messages, and Supabase error code reference.

# Error Handling Architecture

## Error Boundary Hierarchy

```
app/
  error.tsx              ← Root error boundary (catches everything)
  (auth)/
    error.tsx            ← Auth section errors
  (dashboard)/
    error.tsx            ← Dashboard errors
    settings/
      error.tsx          ← Settings-specific errors (optional)
  (content)/
    error.tsx            ← Content section errors
```

## Error Boundary Template

```tsx
"use client"

export default function Error({
  error,
  reset,
}: {
  error: Error & { digest?: string }
  reset: () => void
}) {
  return (
    <div className="flex flex-col items-center gap-4 p-8">
      <h2>Something went wrong</h2>
      <p>We're looking into it. Please try again.</p>
      <button onClick={() => reset()}>Try again</button>
    </div>
  )
}
```

## Supabase Error Codes

| Code | Meaning | Action |
|------|---------|--------|
| 23505 | Unique violation | "This item already exists" |
| 42501 | RLS violation | "You don't have permission" |
| PGRST116 | No rows returned | Call notFound() |
| 23503 | FK violation | "Referenced item not found" |

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
