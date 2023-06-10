# Locators

The Playwright team highly encourages the usage of "user-first" locators to be as close to the end-user experience as possible. The recommended locators are:

- `page.getByRole()` (user-first)
- `page.getByText()` (user-first)
- `page.getByLabel()` (user-first)
- `page.getByPlaceholder()` (user-first)
- `page.getByAltText()` (user-first)
- `page.getByTitle()` (user-first)
- `page.getByTestId()` ("qa-first")

If these user-first locators don't fit your need, CSS selector based locators work (`page.locator('.cta')`), too.

[Check other locators](https://playwright.dev/docs/other-locators).

### Important locator characteristics

Playwright Test's locators include core functionality you must be aware of.

#### Locators are strict

A locator throws an exception if it matches multiple DOM elements.

```typescript
await page.getByRole("link").click();
```

```bash
locator.click: Error: strict mode violation: getByRole('link') resolved to 9 elements:
    1) <a href="/users" data-phx-link="redirect" data-phx-…>…</a> aka getByRole('link', { name: 'Customers' })
    2) <a href="/admins" data-phx-link="redirect" data-phx…>…</a> aka getByRole('link', { name: 'Admins' })
    3) <a href="/site_articles" data-phx-link="redirect" d…>…</a> aka getByRole('link', { name: 'Site Articles' })
// ...
```

> **Warning**
> Playwright started with interaction methods on the `page` object such as `page.click(selector)`. These are discouraged and deprecated by now.

#### Locators are lazy

Every time a locator is used for an action, an up-to-date DOM element is located on the page.

```typescript
const usernameSearch = page.getByPlaceholder("Search by User Name1");
console.log(`Locator is not used yet`);
await usernameSearch.fill("123");
```

> **Note**
> The default timeout is 30s and can be changed on a project basis in your Playwright config under `actionTimeout`.

#### Locators can be chained

To narrow down your selection you can always filter and chain locators.

```typescript
await page.locator("tbody").getByRole("row").count();
```

---

## 🏗️ Action item

- [ ] Set actionTimeout for your project
- [ ] Check that locator are strict and lazy
- [ ] Create 1 more test which would search for user with name `myrtice.gerlach` and check that it's only 1 row with this name

---


Let's speak more about [polling](./05-polling.md)!
