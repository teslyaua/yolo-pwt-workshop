# Handling flaky tests with Polling

### Polling: expect.poll
You can convert any synchronous expect to an asynchronous polling one using expect.poll. Polling generally means checking status, or in the case of the playwright, it can be for checking Response. Using the expect, we can convert any synchronous expect to be asynchronous expect.poll

### Polling: expect.toPass

You can retry blocks of code until they are passing successfully.
You can also specify custom timeout for retry intervals

```typescript
await expect(async () => {
  <your code>
  expect(rowNumber).toBe(1);
}).toPass({
  // Probe, wait 1s, probe, wait 2s, probe, wait 10s, probe, wait 10s, probe, .... Defaults to [100, 250, 500, 1000].
  intervals: [1_000, 2_000, 10_000],
  timeout: 60_000
});
```

### Retries
Test retries are a way to automatically re-run a test when it fails. This is useful when a test is flaky and fails intermittently. 



## 🏗️ Action item

- [ ] Add polling for waiting for "Admin could search user by name"
- [ ] Make intetional 1 test flaky and check that it works
- [ ] Add tests for search by User ID and emal

**Additional Task**

- [ ] Check that Status of user is active


-----


Let's speak more about [structure](./06-adding-structure.md)!