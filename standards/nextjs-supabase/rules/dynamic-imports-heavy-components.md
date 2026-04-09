# Use dynamic imports for heavy client components

**Impact:** MEDIUM | **Category:** performance | **Effort:** small

> Use next/dynamic to code-split large client-only components like editors, charts, and maps.

## Why This Matters

`next/dynamic` with `ssr: false` ensures heavy client components are:
- **Code-split** — loaded as a separate chunk
- **Lazy loaded** — only when the component mounts
- **Server-safe** — won't break SSR

## Good

```typescript
import dynamic from "next/dynamic"

const MarkdownEditor = dynamic(
  () => import("./markdown-editor"),
  { loading: () => <Skeleton />, ssr: false }
)
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
