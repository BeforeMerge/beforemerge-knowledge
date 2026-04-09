# Enable RLS on every table

**Impact:** CRITICAL | **Category:** security | **Effort:** trivial

> Every table must have Row Level Security enabled. Tables without RLS are fully accessible via the anon key.

## Why This Matters

Supabase exposes your database via a REST API using the anon key (which is public). Without RLS:
- Any browser can query the table directly
- No authentication required
- Full CRUD access to all rows

## Good

```sql
CREATE TABLE public.scans (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  organization_id uuid NOT NULL REFERENCES organization(id)
);

ALTER TABLE public.scans ENABLE ROW LEVEL SECURITY;

CREATE POLICY "Org members can view scans"
  ON public.scans FOR SELECT
  USING (is_org_member(organization_id));
```

## Bad

```sql
CREATE TABLE public.scans (...);
-- Forgot to enable RLS — table is fully public!
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
