# API Testing Examples

## 1) Cypress `cy.request` example
```js
// cypress/e2e/api/users.cy.js
describe('Users API', () => {
  it('creates and validates a user', () => {
    cy.request('POST', '/api/users', {
      email: `user_${Date.now()}@example.com`,
      password: 'Str0ng!Pass',
      country: 'US'
    }).then(res => {
      expect(res.status).to.be.oneOf([200,201]);
      expect(res.body).to.have.property('id');
      const id = res.body.id;
      cy.request('GET', `/api/users/${id}`).its('status').should('eq', 200);
    });
  });
});
```

## 2) Postman Collection (minimal)
Save as `postman/Users.postman_collection.json` and import to Postman.

```json
{
  "info": {
    "name": "Users API",
    "_postman_id": "00000000-0000-0000-0000-000000000000",
    "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
  },
  "item": [
    {
      "name": "Create User",
      "request": {
        "method": "POST",
        "header": [{ "key": "Content-Type", "value": "application/json" }],
        "url": "{{baseUrl}}/api/users",
        "body": {
          "mode": "raw",
          "raw": "{\n  \"email\": \"{{email}}\",\n  \"password\": \"Str0ng!Pass\",\n  \"country\": \"US\"\n}"
        }
      }
    }
  ]
}
```
