# Use server components for data fetching by default

**Impact:** HIGH | **Category:** performance | **Effort:** medium

> Fetch data in async server components instead of client-side useEffect + fetch patterns.

## Why This Matters

Server Components fetch data at render time with:
- **Zero client JS** — data fetching code never reaches the browser
- **No loading spinners** — page renders with data already present
- **No exposed API** — no public endpoints for attackers to discover

## Good

```tsx
// Server component — async, no "use client"
export default async function RulesPage() {
  const rules = await getRules()
  return <RuleList rules={rules} />
}
```

## Bad

```tsx
"use client"
export default function RulesPage() {
  const [rules, setRules] = useState([])
  useEffect(() => {
    fetch("/api/rules").then(r => r.json()).then(setRules)
  }, [])
  if (!rules.length) return <Spinner />
  return <RuleList rules={rules} />
}
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
