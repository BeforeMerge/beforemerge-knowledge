# Use next/image for all images

**Impact:** HIGH | **Category:** performance | **Effort:** small

> Use the Image component from next/image instead of raw HTML img tags. It auto-optimizes format, size, and loading.

## Why This Matters

`next/image` provides:
- **Format optimization** — serves WebP/AVIF when supported
- **Responsive sizing** — generates multiple sizes for different screens
- **Lazy loading** — images load only when visible
- **CLS prevention** — reserves space to prevent layout shift

## Good

```tsx
import Image from "next/image"

<Image src="/hero.jpg" alt="Hero" width={800} height={400} />
```

## Bad

```tsx
<img src="/hero.jpg" alt="Hero" />  // No optimization!
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
