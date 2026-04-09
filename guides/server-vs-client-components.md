# Server Components vs Client Components — The Decision Framework

> When to use server components and when to reach for "use client". Flowchart, refactoring patterns, and performance implications.

# Server Components vs Client Components

Next.js App Router defaults to Server Components. This guide helps you decide when to use each.

## The Rule

**Server Components by default. Client Components only when you need browser interactivity.**

## When to Use Server Components

- Fetching data from database or API
- Rendering static content
- Accessing server-only resources (env vars, filesystem)
- Components that don't need user interaction

## When to Use Client Components

- Event handlers (onClick, onChange, onSubmit)
- React hooks (useState, useEffect, useRef, useContext)
- Browser APIs (window, localStorage, navigator)
- Third-party libraries that use browser APIs

## The Boundary Pattern

Push `"use client"` as low as possible in the component tree.

```tsx
// page.tsx — SERVER COMPONENT (default)
export default async function RulePage({ params }) {
  const rule = await getRule(params.slug)  // Server-side fetch
  return (
    <div>
      <h1>{rule.title}</h1>           {/* Server rendered */}
      <p>{rule.description}</p>        {/* Server rendered */}
      <RuleBody body={rule.body} />     {/* Server rendered */}
      <LikeButton ruleId={rule.id} />   {/* Client component */}
    </div>
  )
}

// components/like-button.tsx — CLIENT COMPONENT (minimal)
"use client"
export function LikeButton({ ruleId }: { ruleId: string }) {
  const [liked, setLiked] = useState(false)
  return <button onClick={() => setLiked(!liked)}>Like</button>
}
```

## Performance Impact

| | Server Component | Client Component |
|---|---|---|
| JS sent to browser | 0 bytes | Full component code |
| Data fetching | Server-side, no API needed | Requires API route or fetch |
| SEO | Fully rendered HTML | Requires hydration |
| Time to Interactive | Instant | After JS loads |
| Can use secrets | Yes | No (browser visible) |

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
