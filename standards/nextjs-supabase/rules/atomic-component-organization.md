# Organize components into atoms, molecules, organisms

**Impact:** MEDIUM | **Category:** quality | **Effort:** medium

> Use atomic design to structure components: atoms (Button, Input), molecules (SearchBar, FormField), organisms (Header, Sidebar).

## Why This Matters

Atomic design creates predictable component hierarchy:
- **Atoms**: Independent, no dependencies (Button, Input, Badge)
- **Molecules**: Combine atoms (SearchBar = Input + Button)
- **Organisms**: Combine molecules (Header = Logo + Nav + SearchBar)

## Good

```
components/
  atoms/
    button.tsx
    input.tsx
    badge.tsx
  molecules/
    search-bar.tsx
    form-field.tsx
  organisms/
    header.tsx
    sidebar.tsx
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
