# Authentication

> Let's speed up test with a storageState.

Playwright executes tests in isolated environments called browser contexts. This isolation model improves reproducibility and prevents cascading test failures. Tests can load existing authenticated state. This eliminates the need to authenticate in every test and speeds up test execution.

More about [Authentication](https://playwright.dev/docs/auth)

### Save storage for you logged in user

Web apps use cookie-based or token-based authentication, where authenticated state is stored as cookies or in local storage. Playwright provides browserContext.storageState([options]) method that can be used to retrieve storage state from authenticated contexts and then create new contexts with prepopulated state.

```typescript
  await backoffice.page
    .context()
    .storageState({ path: "storageStates/ygfAdminSavedStorage.json" });
```

Add storageState  to your test


# Tag tests
Filter to only run tests with a title matching one of the patterns. For example, passing `grep`: /cart/ should only run tests with "cart" in the title. You could also use `grepInvert` to filter to only run tests with a title not matching one of the patterns. 

### Add grep
```typescript
extendedTest(
  "@smoke | Admin could search user by name"...

----------
Add this to playwright.config.ts 
 grep: /@smoke/

```

# Gmail Testing
During the testing, user flows such as “Recover Password”, “Invite user”, “Get OTP” etc, need to be covered by reading the email body. 
Since our company uses google services already, one of the options is to use Gmail API. Gmail API is a RESTful API that can be used to access Gmail mailboxes and send mail. Here is a step-by-step guide on configuring it for JS/TS automation tests.

[How to deal with emails in test automation: Gmail](https://coingaming.atlassian.net/wiki/spaces/CGQA/pages/9644867967/How+to+deal+with+emails+in+test+automation+Gmail)

## 🏗️ Action item

- [ ] Rewrite your tests with saved storage
- [ ] Add tags for test and run specific group of tests
- [ ] Add test for recover_username with reading email


-----
