# Remember the Supabase query builder is immutable

**Impact:** HIGH | **Category:** quality | **Effort:** trivial

> Supabase's .eq(), .filter(), .order() return new builder objects. Calling them without reassignment does nothing.

## Why This Matters

The query builder is **immutable** — each method returns a new object.

## Good

```typescript
let query = supabase.from("scans").select("*")
query = query.eq("status", "active")  // reassign!
query = query.order("created_at", { ascending: false })
const { data } = await query
```

## Bad

```typescript
let query = supabase.from("scans").select("*")
query.eq("status", "active")  // DOES NOTHING — return value discarded!
const { data } = await query   // returns ALL scans, not just active
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
