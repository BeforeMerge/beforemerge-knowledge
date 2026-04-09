# Query Supabase directly in server components — skip API routes

**Impact:** HIGH | **Category:** architecture | **Effort:** small

> Server components can query Supabase directly. Don't create API route middlemen just to proxy Supabase queries.

## Why This Matters

Server components run on the server — they can query Supabase directly. Creating an API route that just calls Supabase and returns the result is unnecessary indirection.

## Good

```typescript
// app/(content)/rules/page.tsx (server component)
const supabase = await createClient()
const { data: rules } = await supabase.from("rules").select("*")
```

## Bad

```typescript
// app/api/rules/route.ts — unnecessary middleman
export async function GET() {
  const { data } = await supabase.from("rules").select("*")
  return Response.json(data)
}

// page.tsx — calls the unnecessary API route
const rules = await fetch("/api/rules").then(r => r.json())
```

**Exception:** API routes ARE needed for: webhooks, external consumers, OAuth callbacks, cron jobs.

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
