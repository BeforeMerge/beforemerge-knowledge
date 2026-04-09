# BeforeMerge Knowledge

Curated, opinionated development standards for modern web stacks. Human-researched, battle-tested, continuously maintained.

## What Is This?

Unlike AI-generated advice that varies with every prompt, these standards are:

- **Researched** from production codebases and official documentation
- **Opinionated** — we make the decision so you don't have to
- **Enforceable** — each standard maps to a scanner rule on [BeforeMerge](https://beforemerge.com)
- **Open** — free to use, adapt, and share (CC BY-NC-SA 4.0)

## Available Standards

### [Next.js + Supabase Standards](standards/nextjs-supabase/)

50+ rules covering the full stack:

| Category | Rules | Highlights |
|----------|-------|------------|
| Project Structure | 8 | Route groups, file naming, server-only imports |
| Data Fetching | 7 | Server components, parallel fetches, error handling |
| Supabase Auth | 8 | Three client types, middleware, service_role protection |
| RLS & Database | 8 | Enable RLS, deny-by-default, helper functions |
| Server Actions | 5 | Auth, validation, org scoping |
| Component Patterns | 5 | Server-first, client boundaries, loading states |
| TypeScript | 2 | Strict mode, no `any` |
| Performance | 2 | next/image, dynamic imports |
| Error Handling | 3 | Error boundaries, structured logging |
| Security | 4 | Hardcoded secrets, input validation, RLS testing |
| Testing | 2 | RLS tests, server action isolation |

### Guides

In-depth articles that explain the _why_ behind the rules:

- [The Three Supabase Clients](guides/three-supabase-clients.md)
- [RLS Policy Design Patterns](guides/rls-policy-patterns.md)
- [Server Components vs Client Components](guides/server-vs-client-components.md)
- [Data Fetching Patterns](guides/data-fetching-patterns.md)
- [Server Action Patterns](guides/server-action-patterns.md)
- [Database Migration Best Practices](guides/database-migration-best-practices.md)
- [Authentication Flow](guides/auth-flow.md)
- [Performance Optimization Checklist](guides/performance-checklist.md)
- [Error Handling Architecture](guides/error-handling-architecture.md)
- [TypeScript Patterns for Supabase](guides/typescript-patterns.md)
- [Testing Supabase Applications](guides/testing-supabase-apps.md)
- [Security Checklist](guides/security-checklist.md)

## Quick Start

### Use with BeforeMerge (recommended)

1. Sign up at [beforemerge.com](https://beforemerge.com)
2. Install the GitHub App
3. Go to Explore > Collections > "Next.js + Supabase Standards"
4. Click **Install** — rules are immediately used in your next scan

### Use standalone

Browse the standards in [`standards/`](standards/) and guides in [`guides/`](guides/). Each rule includes:

- Why it matters
- Good and bad code examples
- Detection hints for automated enforcement

## Contributing

We welcome contributions! Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting a pull request.

First-time contributors must accept our Contributor License Agreement (CLA) via the CLA Assistant bot on your first PR.

## License

This work is licensed under [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/).

You are free to share and adapt this material for non-commercial purposes, with attribution and under the same license.

## Disclaimer

> THE CONTENT IN THIS REPOSITORY IS PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED. BEFOREMERGE AND ITS CONTRIBUTORS SHALL NOT BE LIABLE FOR ANY DAMAGES ARISING FROM THE USE OF THIS CONTENT. THIS CONTENT REPRESENTS OPINIONATED BEST PRACTICES AND SHOULD BE EVALUATED IN THE CONTEXT OF YOUR SPECIFIC PROJECT, TEAM, AND REQUIREMENTS. ALWAYS REVIEW AND TEST ANY RECOMMENDATIONS BEFORE APPLYING THEM TO PRODUCTION SYSTEMS.

## About BeforeMerge

[BeforeMerge](https://beforemerge.com) is a code review platform that enforces development standards through automated scanning, AI-powered fix suggestions, and curated knowledge. Built by [Chykalophia](https://chykalophia.com).
