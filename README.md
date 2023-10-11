# edu-react-intro-2

## Create Project

```bash
npm install --save-dev cypress
npm pgk set scripts.cypress:open="cypress open"
mkdir -p ./cypress/integration
touch ./cypress/integration/login_spec.js
```



## Create ./cypress/integration/login_spec.js

```
cat > ./cypress/integration/login_spec.js << 'EOF'
describe('Login Tests', () => {

  beforeEach(() => {
    // Visit the app before each test
    cy.visit('http://localhost:3000'); // Adjust URL accordingly
  });

  it('Main Flow: user can login with correct credentials', () => {
    cy.get('input[placeholder="Email"]').type('user@example.com');
    cy.get('input[placeholder="Password"]').type('password');
    cy.get('button').contains('Log In').click();

    // Check that "Log Out" button is shown after logging in
    cy.get('button').contains('Log Out').should('be.visible');
  });

  it('Alternate Flow: user cannot login with incorrect credentials', () => {
    cy.get('input[placeholder="Email"]').type('wrong@example.com');
    cy.get('input[placeholder="Password"]').type('wrongpassword');
    cy.get('button').contains('Log In').click();

    // Check that error message is shown
    cy.get('p').contains('Not authorized').should('be.visible');
    // Check that "Log Out" button is not shown
    cy.get('button').contains('Log Out').should('not.exist');
  });

  it('Main Flow: user can logout after logging in', () => {
    cy.get('input[placeholder="Email"]').type('user@example.com');
    cy.get('input[placeholder="Password"]').type('password');
    cy.get('button').contains('Log In').click();
    // Check that "Log Out" button is shown
    cy.get('button').contains('Log Out').click();

    // Check that "Log In" button is shown again after logging out
    cy.get('button').contains('Log In').should('be.visible');
  });
});
EOF
```





