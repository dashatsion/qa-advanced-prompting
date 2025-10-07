# Playwright Example: Login (Page Object)

## Install
```bash
npm init -y
npm i -D @playwright/test
npx playwright install
```

## Files

**`tests/pages/LoginPage.ts`**
```ts
import { Page } from '@playwright/test';

export class LoginPage {
  constructor(private page: Page) {}
  async goto() { await this.page.goto('/login'); }
  email = () => this.page.locator('[data-cy=email]');
  password = () => this.page.locator('[data-cy=password]');
  submit = () => this.page.locator('[data-cy=submit]');
  error = () => this.page.locator('[data-cy=error]');
}
```

**`tests/login.spec.ts`**
```ts
import { test, expect } from '@playwright/test';
import { LoginPage } from './pages/LoginPage';

test.describe('Login', () => {
  test.beforeEach(async ({ page }) => {
    const login = new LoginPage(page);
    await login.goto();
  });

  test('logs in with valid credentials', async ({ page }) => {
    const login = new LoginPage(page);
    await login.email().fill(process.env.USER_EMAIL || '');
    await login.password().fill(process.env.USER_PASSWORD || '');
    await login.submit().click();
    await expect(page).toHaveURL(/.*dashboard/);
  });

  test('shows error on invalid credentials', async ({ page }) => {
    const login = new LoginPage(page);
    await login.email().fill('invalid@example.com');
    await login.password().fill('wrong');
    await login.submit().click();
    await expect(login.error()).toContainText('Invalid credentials');
  });
});
```
