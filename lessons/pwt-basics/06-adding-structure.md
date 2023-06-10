# Page object models

> Let's structure and configure tests.

Large test suites can be structured to optimize ease of authoring and maintenance. Page object models are one such approach to structure your test suite.

Page objects simplify authoring by creating a higher-level API which suits your application and simplify maintenance by capturing element selectors in one place and create reusable code to avoid repetition.

### Create page objects

You could pages wrapper to easy use

```typescript
export const Backoffice = (page: Page) => ({
  page: page,
  loginPage: loginPage(page),
});
```

Add extendedTest fixture to your test

```typescript
const extendedTest = test.extend<{ backoffice: ReturnType<typeof Backoffice> }>(
  {
    backoffice: async ({ page }, use) => {
      await use(Backoffice(page));
    },
  }
);

```

### Add enums
```typescript
export enum Operators {
  test_operator = "test_operator",
  coingaming = "coingaming",
  ygf = "ygf",
}

```

### Add models
```typescript
export class Admin {
  adminName: string;
  adminPassword: string;
  operatorName: Operators;
  adminEmail: string;

  constructor(
    adminName: string,
    adminPassword: string,
    operatorName: Operators,
  ) {
    this.adminName = adminName;
    this.adminPassword = adminPassword;
    this.operatorName = operatorName;
  }
}

export const ygfAdmin = new Admin(
  "iurii.teslia",
  "123",
  Operators.ygf
);

```

### Add beforeEach hook and update tests
Declares a beforeEach hook that isv executed before each test.


```typescript
extendedTest.beforeEach(async ({ backoffice }) => {
  await backoffice.loginPage.open();
  await backoffice.loginPage.login(ygfAdmin);
});

extendedTest("Admin could search user by name", async ({ backoffice }) => {
  await backoffice.customersPage.searchByUserName(searchOptions.userName, "myrtice.gerlach")
});

```

## 🏗️ Action item

- [ ] Rewrite your tests with PO structrure 
- [ ] Create enum for searchOption
- [ ] Add customersPage


-----
