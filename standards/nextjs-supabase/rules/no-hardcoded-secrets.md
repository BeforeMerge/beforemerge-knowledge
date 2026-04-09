# Never hardcode API keys or secrets in source code

**Impact:** CRITICAL | **Category:** security | **Effort:** trivial

> Always use environment variables for API keys, database credentials, and other secrets.

## Why This Matters

Hardcoded secrets are:
- **In git history forever** — even after removal
- **Visible in CI logs** — build output may print them
- **In client bundles** — if in a "use client" file
- **Hard to rotate** — requires code change + deployment

## Good

```typescript
const apiKey = process.env.ANTHROPIC_API_KEY
```

## Bad

```typescript
const apiKey = "sk-ant-api03-..."  // NEVER
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
