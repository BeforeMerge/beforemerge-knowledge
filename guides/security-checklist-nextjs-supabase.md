# Security Checklist for Next.js + Supabase

> Environment variable management, SSRF prevention, input validation, rate limiting, CSP headers, and service role key protection.

# Security Checklist

## Environment Variables
- [ ] Service role key is NOT in `NEXT_PUBLIC_` vars
- [ ] `.env.local` is in `.gitignore`
- [ ] `.env.example` has all required vars (no values)
- [ ] No secrets hardcoded in source code
- [ ] Secrets not logged in error messages

## Supabase
- [ ] RLS enabled on ALL tables
- [ ] No `USING (true)` on private tables
- [ ] `is_org_member()` helper used consistently
- [ ] Admin client used only for writes with requireAuth()
- [ ] Generated types used for query safety

## Server Actions
- [ ] `requireAuth()` is first call in every action
- [ ] All inputs validated with Zod
- [ ] `organization_id` explicitly set on all mutations
- [ ] Error messages don't expose internals

## Web Security
- [ ] CSP headers configured
- [ ] SSRF protection on user-provided URLs
- [ ] Rate limiting on public endpoints
- [ ] HTTPS-only cookies for sessions
- [ ] `server-only` package used on sensitive modules

## Dependencies
- [ ] Dependencies pinned to exact versions
- [ ] `npm audit` runs in CI
- [ ] No known vulnerabilities in production deps

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
