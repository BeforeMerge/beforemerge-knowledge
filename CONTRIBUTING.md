# Contributing to BeforeMerge Knowledge

Thank you for your interest in contributing to the BeforeMerge Knowledge repository! This guide explains how to contribute new standards, improve existing ones, and submit knowledge articles.

## Contributor License Agreement (CLA)

**First-time contributors must accept our CLA.** When you open your first pull request, the CLA Assistant bot will prompt you to sign. This is a one-time process.

By signing the CLA, you agree that:

1. Your contributions are your original work
2. You grant BeforeMerge the right to use and relicense contributions
3. You understand the CC BY-NC-SA 4.0 licensing terms

## What We Accept

### New Standards Rules

- Opinionated best practices backed by real-world evidence
- Rules with clear "good" and "bad" code examples
- Detection hints (grep patterns, semgrep rules) when possible
- Rules relevant to supported stacks (Next.js, Supabase, TypeScript, React)

### Knowledge Articles

- In-depth guides explaining the _why_ behind standards
- Architecture decision guides with trade-off analysis
- Migration guides (e.g., "Moving from Pages Router to App Router")
- Security guides with practical examples

### Improvements

- Better code examples
- Corrected detection patterns
- Updated information for new framework versions
- Typo and clarity fixes

## What We Don't Accept

- AI-generated content without human review and editing
- Framework-agnostic advice (we're opinionated about specific stacks)
- Standards that only apply to one team's preferences without broader value
- Content that promotes specific commercial products (except the frameworks themselves)

## Submission Process

1. **Fork** the repository
2. **Create a branch** for your change: `git checkout -b add/rule-name` or `fix/article-name`
3. **Write your content** following the templates below
4. **Submit a PR** with a clear description of what and why
5. **Accept the CLA** (first-time only)
6. **Address review feedback** — we may suggest changes for consistency

## Rule Template

```markdown
### Rule Title (imperative: "Use server components by default")

**Impact:** CRITICAL | HIGH | MEDIUM | LOW
**Category:** security | performance | architecture | quality
**Effort:** trivial | small | medium | large | complex

**Why it matters:** 1-2 sentences explaining the consequence of not following this rule.

#### Good

\`\`\`typescript
// Example of correct code
\`\`\`

#### Bad

\`\`\`typescript
// Example of incorrect code with comment explaining why
\`\`\`

**Detection:** How a scanner could check for this (grep pattern, file check, etc.)
```

## Code of Conduct

Be respectful, constructive, and focused on making the standards better. We're building a resource for the community — debates about standards are welcome, personal attacks are not.

## Questions?

Open a GitHub Discussion or reach out at [beforemerge.com/contact](https://beforemerge.com/contact).
