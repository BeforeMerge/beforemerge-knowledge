# Testing Supabase Applications

> Testing RLS policies, server action isolation, integration tests with real database, and E2E patterns.

# Testing Supabase Applications

## 1. Test RLS Policies

RLS bugs are silent data breaches. Test them explicitly.

```typescript
describe("RLS: scans table", () => {
  test("user can only see own org scans", async () => {
    const client = await createAuthClient(userA)
    const { data } = await client.from("scans").select("*")
    expect(data.every(s => s.organization_id === orgA.id)).toBe(true)
  })

  test("user cannot see other org scans", async () => {
    const client = await createAuthClient(userA)
    const { data } = await client
      .from("scans")
      .select("*")
      .eq("organization_id", orgB.id)
    expect(data).toHaveLength(0)
  })
})
```

## 2. Test Server Actions

Server actions are async functions — test them without UI.

```typescript
test("createRule requires auth", async () => {
  vi.mocked(requireAuth).mockRejectedValue(new Error("Unauthorized"))
  await expect(createRule(mockData)).rejects.toThrow()
})
```

## 3. Integration Tests

Use a real Supabase instance, not mocks.

```typescript
// Use local Supabase: npx supabase start
const supabase = createClient(LOCAL_URL, LOCAL_ANON_KEY)
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
