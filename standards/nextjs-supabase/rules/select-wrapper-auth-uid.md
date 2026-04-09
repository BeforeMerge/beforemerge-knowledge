# Use (select auth.uid()) instead of auth.uid() in policies

**Impact:** MEDIUM | **Category:** performance | **Effort:** trivial

> Wrapping auth.uid() in (select ...) ensures it's evaluated once per query instead of once per row.

## Why This Matters

PostgreSQL may evaluate `auth.uid()` per-row without the subquery wrapper. On a table with millions of rows, this adds overhead.

## Good

```sql
CREATE POLICY "own_data" ON profiles
  FOR SELECT USING (id = (SELECT auth.uid()));
```

## Bad

```sql
CREATE POLICY "own_data" ON profiles
  FOR SELECT USING (id = auth.uid());  -- evaluated per row
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
