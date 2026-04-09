# Use kebab-case for file and directory names

**Impact:** MEDIUM | **Category:** quality | **Effort:** small

> Name files and directories in kebab-case (lowercase with hyphens) to avoid cross-platform case sensitivity issues.

## Why This Matters

Case sensitivity differs between operating systems:
- **macOS/Windows**: case-insensitive (MyFile.tsx = myfile.tsx)
- **Linux**: case-sensitive (MyFile.tsx ≠ myfile.tsx)

Using kebab-case eliminates this entire class of bugs.

## Good

```
lib/rule-actions.ts
components/molecules/fancy-select.tsx
app/(content)/rules/[slug]/page.tsx
```

## Bad

```
lib/RuleActions.ts
components/molecules/FancySelect.tsx
```

**Exception:** React component files can use PascalCase if your team prefers it, but be consistent.

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
