# Validate and sanitize all user input

**Impact:** HIGH | **Category:** security | **Effort:** small

> Use Zod or similar validation on all API routes and server actions. Never pass raw user input to database queries.

## Why This Matters

User input is untrusted. Validate at the boundary:

```typescript
import { z } from "zod"

const schema = z.object({
  email: z.string().email(),
  name: z.string().min(1).max(100),
  role: z.enum(["member", "admin"]),
})

export async function inviteUser(input: unknown) {
  const data = schema.parse(input)  // Throws on invalid input
  // ... safe to use data
}
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
