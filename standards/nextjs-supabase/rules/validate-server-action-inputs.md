# Validate all server action inputs at the boundary

**Impact:** HIGH | **Category:** security | **Effort:** small

> Server actions are public HTTP endpoints. Validate all inputs with Zod or similar before any database operation.

## Why This Matters

Server actions can be called by anyone — they're public HTTP endpoints. Never trust the input.

## Good

```typescript
import { z } from "zod"

const CreateRuleSchema = z.object({
  title: z.string().min(1).max(200),
  category: z.enum(["security", "performance", "architecture", "quality"]),
  impact: z.enum(["CRITICAL", "HIGH", "MEDIUM", "LOW"]),
})

export async function createRule(input: unknown) {
  const { orgId } = await requireAuth()
  const data = CreateRuleSchema.parse(input)
  // ... safe to use data
}
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
