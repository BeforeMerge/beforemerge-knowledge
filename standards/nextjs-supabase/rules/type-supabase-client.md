# Type your Supabase client with generated database types

**Impact:** MEDIUM | **Category:** quality | **Effort:** small

> Use supabase gen types typescript to generate types from your schema, then pass them as a generic: createClient<Database>().

## Why This Matters

Generated types give you:
- **Autocomplete** for table and column names
- **Type errors** for wrong column types
- **Compile-time safety** instead of runtime errors

## How to Generate

```bash
npx supabase gen types typescript --project-id YOUR_PROJECT_ID > database.types.ts
```

## Good

```typescript
import { Database } from "./database.types"

const supabase = createServerClient<Database>(url, key, { ... })
const { data } = await supabase.from("rules").select("title, slug")
// data is typed: { title: string; slug: string }[]
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
