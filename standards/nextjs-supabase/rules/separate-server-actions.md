# Keep server actions in dedicated files

**Impact:** HIGH | **Category:** architecture | **Effort:** small

> Place server actions in separate *-actions.ts files rather than inline in page components.

## Why This Matters

Server actions in dedicated files are:
- **Reusable** across multiple pages
- **Testable** in isolation (no component rendering needed)
- **Clear** about what mutations exist

## Good

```typescript
// lib/rule-actions.ts
"use server"

export async function createRule(data: FormData) {
  const { orgId } = await requireAuth()
  // ... create rule scoped to org
}
```

## Bad

```typescript
// app/rules/page.tsx
export default function RulesPage() {
  async function handleCreate() {
    "use server"
    // action logic mixed with UI
  }
  return <form action={handleCreate}>...</form>
}
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
