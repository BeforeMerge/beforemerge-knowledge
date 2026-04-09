# Server components by default — client only when needed

**Impact:** HIGH | **Category:** performance | **Effort:** medium

> Only add "use client" for event handlers, useState/useEffect, browser APIs, or client-only libraries. Everything else should be a server component.

## Why This Matters

Server components have **zero JS bundle cost**. Only use `"use client"` when you need:
- Event handlers (onClick, onChange)
- React hooks (useState, useEffect, useRef)
- Browser APIs (window, localStorage)
- Client-only libraries (chart libraries, map libraries)

## Decision Flowchart

```
Does it need interactivity? → Yes → "use client"
                              → No  → Server component (default)
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
