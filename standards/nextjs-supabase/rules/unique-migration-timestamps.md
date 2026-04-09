# Use unique, timestamped migration filenames

**Impact:** HIGH | **Category:** quality | **Effort:** trivial

> Migration files must have unique timestamps: YYYYMMDDHHMMSS_description.sql. Supabase errors on duplicate versions.

## Why This Matters

Supabase tracks applied migrations in `schema_migrations`. Duplicate timestamps cause:
- Failed `supabase db push`
- Manual cleanup required
- Deployment blocked

## Good

```
20260409120000_create_audit_rules.sql
20260409120001_create_standards_scores.sql
20260409120002_create_convention_rules.sql
```

## Bad

```
20260409120000_create_audit_rules.sql
20260409120000_create_standards_scores.sql  # DUPLICATE timestamp!
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
