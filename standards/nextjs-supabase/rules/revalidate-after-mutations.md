# Use revalidatePath after server action mutations

**Impact:** HIGH | **Category:** quality | **Effort:** trivial

> Call revalidatePath() or revalidateTag() after insert/update/delete operations to refresh cached pages.

## Why This Matters

Next.js caches server component renders. After a mutation, the cached version is stale.

## Good

```typescript
"use server"
import { revalidatePath } from "next/cache"

export async function updateRule(id: string, data: RuleData) {
  const supabase = createAdminClient()
  await supabase.from("rules").update(data).eq("id", id)
  revalidatePath("/rules")
  revalidatePath(`/rules/${data.slug}`)
}
```

## Bad

```typescript
export async function updateRule(id: string, data: RuleData) {
  await supabase.from("rules").update(data).eq("id", id)
  // No revalidation — UI shows old data!
}
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
