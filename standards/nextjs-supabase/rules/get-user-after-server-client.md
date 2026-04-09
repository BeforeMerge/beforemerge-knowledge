# Call auth.getUser() immediately after creating the server client in middleware

**Impact:** CRITICAL | **Category:** security | **Effort:** trivial

> Per Supabase docs: do not run code between createServerClient and supabase.auth.getUser(). A simple mistake could cause random logouts.

## Why This Matters

This is a documented Supabase requirement. The auth session must be refreshed immediately after client creation in middleware.

## Good

```typescript
// middleware.ts
const supabase = createServerClient(url, key, { cookies: { ... } })

// IMPORTANT: Call getUser() IMMEDIATELY
const { data: { user } } = await supabase.auth.getUser()

if (!user && !isPublicRoute(request.nextUrl.pathname)) {
  return NextResponse.redirect(new URL("/login", request.url))
}
```

## Bad

```typescript
const supabase = createServerClient(url, key, { cookies: { ... } })

// DON'T put code here — causes random logouts!
const someData = await doSomething()

const { data: { user } } = await supabase.auth.getUser()
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
