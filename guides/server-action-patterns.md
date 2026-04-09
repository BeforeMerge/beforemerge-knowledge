# Server Action Patterns — Auth, Validation, Error Handling

> Complete guide to writing production server actions with requireAuth, Zod validation, structured error handling, and revalidation.

# Server Action Patterns

## The Template

Every server action should follow this pattern:

```typescript
"use server"

import { z } from "zod"
import { requireAuth } from "@/lib/action-auth"
import { createAdminClient } from "@/lib/supabase/admin"
import { revalidatePath } from "next/cache"

const InputSchema = z.object({
  title: z.string().min(1).max(200),
  category: z.enum(["security", "performance", "architecture", "quality"]),
})

export async function createRule(input: unknown) {
  // 1. Auth
  const { orgId, userId } = await requireAuth()

  // 2. Validate
  const data = InputSchema.parse(input)

  // 3. Mutate
  const admin = createAdminClient()
  const { data: rule, error } = await admin
    .from("rules")
    .insert({ ...data, organization_id: orgId, created_by: userId })
    .select()
    .single()

  if (error) {
    return { success: false, error: error.message }
  }

  // 4. Revalidate
  revalidatePath("/rules")

  // 5. Return
  return { success: true, data: rule }
}
```

## Key Rules

1. **requireAuth() first** — always
2. **Validate input** — never trust FormData
3. **Scope to org** — always include organization_id
4. **Admin client for writes** — createClient for reads
5. **Revalidate all paths** — not just the current page
6. **Return structured results** — { success, data/error }

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
