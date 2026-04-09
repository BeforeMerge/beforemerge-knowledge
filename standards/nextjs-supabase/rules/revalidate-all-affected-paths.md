# Revalidate all affected paths after mutations

**Impact:** MEDIUM | **Category:** quality | **Effort:** trivial

> A rule update affects /rules, /rules/[slug], the dashboard, and possibly the explore page. Revalidate all of them.

## Why This Matters

Content often appears on multiple pages. Revalidating only one leaves others stale.

## Good

```typescript
export async function updateRule(slug: string, data: RuleData) {
  await admin.from("rules").update(data).eq("slug", slug)
  revalidatePath("/rules")
  revalidatePath(`/rules/${slug}`)
  revalidatePath("/explore")
  revalidatePath("/")
}
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
