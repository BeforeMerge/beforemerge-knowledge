# Handle Supabase query errors explicitly

**Impact:** HIGH | **Category:** quality | **Effort:** small

> Always check the error field from Supabase queries. The client returns { data, error } and never throws.

## Why This Matters

Supabase client methods return `{ data, error }` — they **never throw**. If you destructure only `data`, errors are silently swallowed.

## Good

```typescript
const { data, error } = await supabase
  .from("rules")
  .select("*")

if (error) {
  log.error({ error }, "Failed to fetch rules")
  throw new Error(`Failed to fetch rules: ${error.message}`)
}

return data
```

## Bad

```typescript
const { data } = await supabase.from("rules").select("*")
return data  // could be null if query failed!
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
