# Database Migration Best Practices for Supabase

> Migration naming, rollback strategies, seeding data, the moddatetime trigger pattern, and index strategy for Supabase PostgreSQL.

# Database Migration Best Practices

## File Naming

Use unique timestamps: `YYYYMMDDHHMMSS_description.sql`

```
20260409120000_create_audit_rules.sql
20260409120001_create_standards_scores.sql
```

## Migration Template

```sql
-- Description: Create audit_rules table for repo health checks
-- Rollback: DROP TABLE audit_rules;

CREATE TABLE public.audit_rules (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  slug text NOT NULL UNIQUE,
  title text NOT NULL,
  -- ... columns
  created_at timestamptz NOT NULL DEFAULT now(),
  updated_at timestamptz NOT NULL DEFAULT now()
);

-- Always enable RLS
ALTER TABLE public.audit_rules ENABLE ROW LEVEL SECURITY;

-- Always add moddatetime trigger
CREATE TRIGGER audit_rules_updated_at
  BEFORE UPDATE ON public.audit_rules
  FOR EACH ROW EXECUTE FUNCTION extensions.moddatetime(updated_at);

-- Always index foreign keys
CREATE INDEX idx_audit_rules_category ON public.audit_rules(category);
```

## Key Patterns

1. **Use `extensions.moddatetime()`** — not `public.handle_updated_at()`
2. **Index all foreign keys** — PostgreSQL doesn't auto-index FKs
3. **Use `ON CONFLICT DO NOTHING`** for seed data — idempotent migrations
4. **Comment rollback SQL** at the top of each migration
5. **Never modify existing migrations** — create new ones instead

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
