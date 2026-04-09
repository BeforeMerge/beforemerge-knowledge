# Test server actions in isolation

**Impact:** HIGH | **Category:** quality | **Effort:** small

> Server actions are async functions. Test them directly without rendering UI. Mock requireAuth() and the Supabase client.

## Why This Matters

Server actions are pure async functions — test them like any other function.

## Good

```typescript
test("createRule requires auth", async () => {
  vi.mocked(requireAuth).mockRejectedValue(new Error("Unauthorized"))
  await expect(createRule(mockData)).rejects.toThrow("Unauthorized")
})

test("createRule inserts with org scope", async () => {
  vi.mocked(requireAuth).mockResolvedValue({ orgId: "org-1", userId: "user-1" })
  await createRule(mockData)
  expect(mockInsert).toHaveBeenCalledWith(
    expect.objectContaining({ organization_id: "org-1" })
  )
})
```

---
*Part of the [Next.js + Supabase Standards](https://beforemerge.com/explore) collection on BeforeMerge.*
