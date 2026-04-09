# Push "use client" boundary as low as possible

**Impact:** HIGH | **Category:** performance | **Effort:** medium

> Don't add "use client" to page or layout files. Extract the interactive part into a small client component.

## Why This Matters

A `"use client"` on a page file makes **everything in that file** client-rendered — including data that could have been fetched on the server.

## Good

```tsx
// components/like-button.tsx — small client component
"use client"
export function LikeButton({ ruleId }: { ruleId: string }) {
  return <button onClick={() => likeRule(ruleId)}>Like</button>
}

// page.tsx — server component (no "use client")
export default async function RulePage({ params }) {
  const rule = await getRule(params.slug)
  return (
    <div>
      <h1>{rule.title}</h1>
      <p>{rule.description}</p>
      <LikeButton ruleId={rule.id} />
    </div>
  )
}
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
