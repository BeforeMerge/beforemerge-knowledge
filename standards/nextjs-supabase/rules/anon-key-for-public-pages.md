# Use the anon key for public-facing pages

**Impact:** HIGH | **Category:** security | **Effort:** small

> Public pages (explore, content detail) should use createReadOnlyClient() with the anon key, not the service_role.

## Why This Matters

RLS is defense-in-depth. Even on public pages, RLS ensures:
- Only `is_published = true` content is visible
- Private org content stays private
- No accidental data exposure from query bugs

## Good

```typescript
// Public explore page
const supabase = createReadOnlyClient()
const { data } = await supabase
  .from("rules")
  .select("*")
  .eq("is_published", true)
  .eq("visibility", "public")
```

## Bad

```typescript
// Using admin client for reads — bypasses RLS!
const admin = createAdminClient()
const { data } = await admin.from("rules").select("*")
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
