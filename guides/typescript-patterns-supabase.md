# TypeScript Patterns for Supabase Applications

> Generated types workflow, type-safe database queries, discriminated unions for state, and generic CRUD helpers.

# TypeScript Patterns for Supabase

## Generated Types

Generate types from your Supabase schema:

```bash
npx supabase gen types typescript --project-id $PROJECT_ID > database.types.ts
```

Use in your client:

```typescript
import { Database } from "./database.types"

const supabase = createServerClient<Database>(url, key, { cookies })
```

Now all queries are type-safe:

```typescript
const { data } = await supabase.from("rules").select("title, slug, impact")
// data type: { title: string; slug: string; impact: string }[]
```

## Helper Types

```typescript
type Tables = Database["public"]["Tables"]
type Rule = Tables["rule"]["Row"]
type RuleInsert = Tables["rule"]["Insert"]
type RuleUpdate = Tables["rule"]["Update"]
```

## Discriminated Unions for State

```typescript
type ScanState =
  | { status: "idle" }
  | { status: "scanning"; progress: number }
  | { status: "complete"; findings: Finding[] }
  | { status: "error"; error: string }
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
