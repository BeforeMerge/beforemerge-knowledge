# Next.js + Supabase Standards

> 50+ opinionated, production-proven best practices for full-stack Next.js (App Router) + Supabase applications.

## Rules by Category

### Security (9 CRITICAL/HIGH rules)
- [Never expose the service_role key](rules/never-expose-service-role-key.md)
- [Enable RLS on every table](rules/enable-rls-every-table.md)
- [Use three distinct Supabase client types](rules/three-client-types.md)
- [Call auth.getUser() immediately in middleware](rules/get-user-after-server-client.md)
- [Never import server-only code in client components](rules/no-server-imports-in-client.md)
- [Store sensitive env vars without NEXT_PUBLIC_ prefix](rules/no-next-public-secrets.md)
- [Write restrictive RLS policies](rules/deny-by-default-policies.md)
- [Scope all mutations to the authenticated org](rules/scope-mutations-to-org.md)
- [Never hardcode API keys or secrets](rules/no-hardcoded-secrets.md)

### Architecture (6 rules)
- [Use route groups to organize app sections](rules/use-route-groups.md)
- [Keep server actions in dedicated files](rules/separate-server-actions.md)
- [Query Supabase directly — skip API routes](rules/skip-api-routes-for-supabase.md)
- [Use a helper function for org-scoped RLS](rules/use-rls-helper-function.md)
- [Use a lib/ directory for shared utilities](rules/lib-directory-for-shared-utils.md)
- [Use SWR/React Query for client-side real-time data](rules/use-swr-for-realtime.md)

### Quality (15 rules)
- [Handle Supabase query errors explicitly](rules/handle-supabase-errors.md)
- [Use revalidatePath after mutations](rules/revalidate-after-mutations.md)
- [Remember the query builder is immutable](rules/query-builder-immutable.md)
- [Use loading.tsx for route-level loading states](rules/use-loading-tsx.md)
- [Use error.tsx for route-level error boundaries](rules/use-error-tsx.md)
- [Enable strict mode in tsconfig.json](rules/enable-strict-mode.md)
- [Never use any — use unknown](rules/no-any-type.md)
- [Use structured logging](rules/structured-logging.md)
- [Use notFound() for invalid dynamic routes](rules/not-found-for-dynamic-routes.md)
- And more...

### Performance (6 rules)
- [Use server components for data fetching](rules/server-components-for-data-fetching.md)
- [Parallelize independent fetches](rules/parallelize-independent-fetches.md)
- [Server components by default](rules/server-components-by-default.md)
- [Push "use client" boundary as low as possible](rules/push-client-boundary-low.md)
- [Use next/image for all images](rules/use-next-image.md)
- [Use dynamic imports for heavy components](rules/dynamic-imports-heavy-components.md)

## Install on BeforeMerge

Install all 50+ rules with one click:

1. Go to [beforemerge.com/explore](https://beforemerge.com/explore)
2. Find "Next.js + Supabase Standards" collection
3. Click **Install**

Rules will be used in your next scan automatically.

## Disclaimer

> This content represents opinionated best practices and should be evaluated in the context of your specific project. Always review and test recommendations before applying to production systems.
