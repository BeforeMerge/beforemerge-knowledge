# Use structured logging — never console.log in production

**Impact:** HIGH | **Category:** quality | **Effort:** small

> Use a structured logger like pino instead of console.log. Structured logs have timestamps, levels, and are filterable.

## Why This Matters

`console.log` in production:
- **Leaks secrets** in error stack traces
- **Can't be filtered** by log level
- **No timestamps** for debugging timing issues
- **No structured data** for log aggregation

## Good

```typescript
import { log } from "./logger"

log.info({ scanId, tool: "semgrep" }, "tool_start")
log.error({ scanId, error: msg }, "scan_failed")
```

## Bad

```typescript
console.log("starting scan...")
console.error(JSON.stringify({ event: "error", details: err }))
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
