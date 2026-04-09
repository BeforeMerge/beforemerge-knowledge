# Write restrictive RLS policies — deny by default

**Impact:** CRITICAL | **Category:** security | **Effort:** small

> RLS defaults to deny all. Only add the specific policies you need. Never use USING (true) on private tables.

## Why This Matters

RLS is deny-by-default. With no policies, nobody can access rows. Add only what you need.

## Good

```sql
-- Only org members can see their own org's data
CREATE POLICY "org_read" ON scans
  FOR SELECT USING (is_org_member(organization_id));

-- Only published public content is visible to anon
CREATE POLICY "public_read" ON rules
  FOR SELECT USING (is_published = true AND visibility = 'public');
```

## Bad

```sql
-- DANGEROUS: Everyone can read everything
CREATE POLICY "anyone_can_read" ON scans
  FOR SELECT USING (true);
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
