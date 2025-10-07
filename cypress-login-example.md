# Cypress Login Example (Page Object Model)

```js
// cypress/pages/LoginPage.js
class LoginPage {
  email() { return cy.get('[data-cy=email]'); }
  password() { return cy.get('[data-cy=password]'); }
  submit() { return cy.get('[data-cy=submit]'); }
  error() { return cy.get('[data-cy=error]'); }
}
export default new LoginPage();
```

```js
// cypress/e2e/login.cy.js
import login from '../pages/LoginPage';

describe('Login', () => {
  beforeEach(() => cy.visit('/login'));

  it('logs in with valid credentials', () => {
    login.email().type(Cypress.env('user_email'));
    login.password().type(Cypress.env('user_password'));
    login.submit().click();
    cy.url().should('include', '/dashboard');
  });

  it('shows an error on invalid credentials', () => {
    login.email().type('invalid@example.com');
    login.password().type('wrong');
    login.submit().click();
    login.error().should('contain.text', 'Invalid credentials');
  });
});
```
