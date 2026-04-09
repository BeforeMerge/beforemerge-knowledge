# Parallelize independent data fetches with Promise.all

**Impact:** HIGH | **Category:** performance | **Effort:** small

> Use Promise.all for independent Supabase queries instead of sequential await chains.

## Why This Matters

Sequential fetches create a waterfall:

```
Query 1: |████████| 200ms
Query 2:          |████████| 200ms
Query 3:                    |████████| 200ms
Total:                                 600ms
```

Parallel fetches overlap:

```
Query 1: |████████| 200ms
Query 2: |████████| 200ms
Query 3: |████████| 200ms
Total:              200ms
```

## Good

```typescript
const [rules, skills, tags] = await Promise.all([
  getRules(),
  getSkills(),
  getTags(),
])
```

## Bad

```typescript
const rules = await getRules()   // waits 200ms
const skills = await getSkills() // waits another 200ms
const tags = await getTags()     // waits another 200ms
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
