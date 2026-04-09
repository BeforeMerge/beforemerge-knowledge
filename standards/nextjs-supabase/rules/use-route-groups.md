# Use route groups to organize app sections

**Impact:** HIGH | **Category:** architecture | **Effort:** medium

> Organize routes using parenthesized layout groups like (auth), (dashboard), (content), (marketing) for separate layouts and clear separation of concerns.

## Why This Matters

Route groups in Next.js App Router allow you to:
- Apply **different layouts** per section (auth has minimal layout, dashboard has sidebar)
- **Organize routes** without affecting the URL structure
- Keep the `app/` directory **scalable** as you add more pages

## Good

```
app/
  (auth)/login/page.tsx
  (dashboard)/overview/page.tsx
  (content)/rules/[slug]/page.tsx
  (marketing)/pricing/page.tsx
```

## Bad

```
app/
  login/page.tsx
  overview/page.tsx
  rules/[slug]/page.tsx
  pricing/page.tsx
```

## How to Fix

Create route groups by wrapping directory names in parentheses. The parentheses are stripped from the URL.

```bash
mkdir -p app/(auth) app/(dashboard) app/(content) app/(marketing)
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
