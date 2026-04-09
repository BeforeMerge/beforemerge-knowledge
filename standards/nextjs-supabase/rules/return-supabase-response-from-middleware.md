# Return the supabaseResponse object unchanged from middleware

**Impact:** HIGH | **Category:** quality | **Effort:** small

> Creating a new NextResponse without copying Supabase cookies breaks session management and causes random logouts.

## Why This Matters

Supabase sets updated session cookies on the response. If you return a different response object, those cookies are lost.

## Good

```typescript
// Always return supabaseResponse
return supabaseResponse

// If you need a custom response:
const myResponse = NextResponse.next({ request })
myResponse.cookies.setAll(supabaseResponse.cookies.getAll())
return myResponse
```

## Bad

```typescript
// Creating new response — session cookies lost!
return NextResponse.next()
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
