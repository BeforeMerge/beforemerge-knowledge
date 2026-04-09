# Use moddatetime triggers for updated_at columns

**Impact:** MEDIUM | **Category:** quality | **Effort:** trivial

> Use database triggers to auto-update updated_at instead of setting it in application code.

## Why This Matters

Database triggers guarantee `updated_at` is always current, regardless of which code path updates the row.

## Good

```sql
CREATE TRIGGER handle_updated_at
  BEFORE UPDATE ON rules
  FOR EACH ROW
  EXECUTE FUNCTION extensions.moddatetime(updated_at);
```

## Bad

```typescript
// Some code paths forget to update the timestamp
await supabase.from("rules").update({
  title: newTitle,
  // forgot updated_at!
})
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
