# Scope all mutations to the authenticated organization

**Impact:** CRITICAL | **Category:** security | **Effort:** trivial

> Every insert/update/delete must include organization_id from requireAuth(). RLS is defense-in-depth, not the only defense.

## Why This Matters

RLS is your safety net, but application-level scoping is your primary defense.

## Good

```typescript
export async function createRule(data: FormData) {
  const { orgId } = await requireAuth()
  await admin.from("rules").insert({
    ...data,
    organization_id: orgId,  // Always scope to org
  })
}
```

## Bad

```typescript
export async function createRule(data: FormData) {
  await admin.from("rules").insert(data)
  // Missing org_id — relies entirely on RLS
}
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
