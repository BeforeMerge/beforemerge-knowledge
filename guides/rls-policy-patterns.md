# RLS Policy Design Patterns for Multi-Tenant Apps

> Common Row Level Security patterns: org-scoped access, public read with auth write, self-service profiles, and anti-patterns to avoid.

# RLS Policy Design Patterns

Row Level Security is the foundation of data isolation in Supabase. This guide covers patterns for multi-tenant applications.

## Pattern 1: Org-Scoped Access

The most common pattern — users can only access data belonging to their organization.

```sql
-- Helper function (create once, use everywhere)
CREATE FUNCTION is_org_member(org_id uuid) RETURNS boolean AS $$
  SELECT EXISTS (
    SELECT 1 FROM profile
    WHERE user_id = (SELECT auth.uid())
    AND organization_id = org_id
  )
$$ LANGUAGE sql SECURITY DEFINER;

-- Apply to every org-scoped table
CREATE POLICY "org_read" ON scans FOR SELECT
  USING (is_org_member(organization_id));

CREATE POLICY "org_insert" ON scans FOR INSERT
  WITH CHECK (is_org_member(organization_id));
```

## Pattern 2: Public Read, Auth Write

For content that's publicly visible but only editable by org members.

```sql
-- Anyone can read published public content
CREATE POLICY "public_read" ON rules FOR SELECT
  USING (is_published = true AND visibility = 'public');

-- Only org members can read their own unpublished content
CREATE POLICY "org_read" ON rules FOR SELECT
  USING (is_org_member(organization_id));

-- Only org members can write
CREATE POLICY "org_write" ON rules FOR INSERT
  WITH CHECK (is_org_member(organization_id));
```

## Pattern 3: Self-Service Profiles

```sql
CREATE POLICY "users_read_own" ON profiles FOR SELECT
  USING (user_id = (SELECT auth.uid()));

CREATE POLICY "users_update_own" ON profiles FOR UPDATE
  USING (user_id = (SELECT auth.uid()));
```

## Anti-Patterns

### Never: USING (true) on private tables
```sql
-- DANGEROUS: Everyone can read everything
CREATE POLICY "open" ON scans FOR SELECT USING (true);
```

### Never: Forgetting RLS on new tables
```sql
CREATE TABLE secret_data (...);
-- FORGOT: ALTER TABLE secret_data ENABLE ROW LEVEL SECURITY;
-- Result: Table is fully public via anon key
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
