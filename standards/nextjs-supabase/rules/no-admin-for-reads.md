# Never use the admin client for reads in server actions

**Impact:** HIGH | **Category:** security | **Effort:** small

> createAdminClient() bypasses RLS. Use it only for writes that need service_role privileges. For reads, use createClient().

## Why This Matters

`createAdminClient()` bypasses RLS — it sees all data. Using it for reads removes your safety net.

## Good

```typescript
export async function getRule(slug: string) {
  const supabase = await createClient()  // RLS enforced
  return supabase.from("rules").select("*").eq("slug", slug).single()
}
```

## Bad

```typescript
export async function getRule(slug: string) {
  const admin = createAdminClient()  // Bypasses RLS!
  return admin.from("rules").select("*").eq("slug", slug).single()
}
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
