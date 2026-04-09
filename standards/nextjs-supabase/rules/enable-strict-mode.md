# Enable strict mode in tsconfig.json

**Impact:** HIGH | **Category:** quality | **Effort:** small

> Set "strict": true in tsconfig.json to catch null errors, implicit any, and type coercion bugs at compile time.

## Why This Matters

Strict mode enables:
- `strictNullChecks` — catch null/undefined access at compile time
- `noImplicitAny` — no silent any types
- `strictFunctionTypes` — correct function type checking

## Good

```json
// tsconfig.json
{
  "compilerOptions": {
    "strict": true
  }
}
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
