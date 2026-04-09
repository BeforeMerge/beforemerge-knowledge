# Never use any — use unknown for truly unknown types

**Impact:** HIGH | **Category:** quality | **Effort:** small

> The any type disables all type checking. Use unknown and narrow the type, or use a specific type.

## Why This Matters

`any` is a type-system escape hatch. It disables ALL checking:

```typescript
const x: any = "hello"
x.foo.bar.baz()  // No error! Crashes at runtime.
```

## Good

```typescript
function processInput(input: unknown) {
  if (typeof input === "string") {
    return input.toUpperCase()  // Safe — narrowed to string
  }
  throw new Error("Expected string")
}
```

## Bad

```typescript
function processInput(input: any) {
  return input.toUpperCase()  // Crashes if input isn't a string
}
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
