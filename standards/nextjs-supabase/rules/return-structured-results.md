# Return structured results from server actions

**Impact:** MEDIUM | **Category:** quality | **Effort:** small

> Return { success: true, data } or { success: false, error } instead of throwing errors from server actions.

## Why This Matters

Structured results are:
- **Predictable** — caller always gets the same shape
- **Debuggable** — error messages are specific
- **Type-safe** — TypeScript can narrow the result

## Good

```typescript
export async function createRule(data: RuleInput) {
  try {
    const { orgId } = await requireAuth()
    const result = await admin.from("rules").insert({ ...data, organization_id: orgId })
    return { success: true, data: result.data }
  } catch (error) {
    return { success: false, error: "Failed to create rule" }
  }
}
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
