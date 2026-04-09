# Use a helper function for org-scoped RLS checks

**Impact:** HIGH | **Category:** architecture | **Effort:** medium

> Create an is_org_member(org_id) SECURITY DEFINER function and use it in all org-scoped RLS policies.

## Why This Matters

A centralized helper function:
- **Single source of truth** for access logic
- **Easy to update** — change one function, all policies use it
- **SECURITY DEFINER** — runs with elevated privileges to check profile table

## Good

```sql
CREATE FUNCTION is_org_member(org_id uuid) RETURNS boolean AS $$
  SELECT EXISTS (
    SELECT 1 FROM profile
    WHERE user_id = auth.uid()
    AND organization_id = org_id
  )
$$ LANGUAGE sql SECURITY DEFINER;

-- All policies use the same helper
CREATE POLICY "org_access" ON scans USING (is_org_member(organization_id));
CREATE POLICY "org_access" ON findings USING (is_org_member(organization_id));
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
