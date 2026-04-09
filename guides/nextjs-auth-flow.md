# Authentication Flow — From OAuth to Protected Page

> End-to-end auth flow: GitHub OAuth callback, session management, middleware protection, and logout handling in Next.js + Supabase.

# Authentication Flow

## Overview

```
User clicks "Sign in with GitHub"
  → Supabase OAuth redirect
  → GitHub authorization
  → Callback to /auth/callback
  → Session cookie set
  → Middleware validates on every request
  → Protected pages render with user context
```

## Middleware (Critical)

```typescript
// middleware.ts
export async function middleware(request: NextRequest) {
  let supabaseResponse = NextResponse.next({ request })
  const supabase = createServerClient(url, key, { cookies: ... })

  // MUST call getUser() immediately after createServerClient
  const { data: { user } } = await supabase.auth.getUser()

  if (!user && isProtectedRoute(request.nextUrl.pathname)) {
    return NextResponse.redirect(new URL("/login", request.url))
  }

  // MUST return supabaseResponse unchanged
  return supabaseResponse
}
```

## Key Rules

1. **getUser() immediately** after createServerClient in middleware
2. **Return supabaseResponse** unchanged (cookies!)
3. **Never cache auth state** — always check on each request
4. **Use requireAuth()** in server actions — middleware protects pages, requireAuth protects mutations

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
