# edu-react-intro-2

## Create Project

```bash
npm install --save-dev cypress
npm pkg set scripts.cypress:open="cypress open"
npm pkg set scripts.cypress="cypress run --browser chrome"
npm pkg set scripts.cypress:chrome="cypress run --browser chrome"
npm pkg set scripts.cypress:firefox="cypress run --browser firefox"
npm pkg set scripts.cypress:edge="cypress run --browser edge"
mkdir -p ./cypress/e2e
mkdir -p  ./cypress/support
touch ./cypress/e2e/login.cy.js
touch ./cypress/support/index.js
```



## Create ./cypress/e2e/login.cy.js

```
cat > ./cypress/e2e/login.cy.js << 'EOF'
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

## Create ./cypress.config.js

```bash
cat > ./cypress/e2e/login.cy.js << 'EOF'
const { defineConfig } = require('cypress');
module.exports = defineConfig({
  e2e: {
    // Folder where Cypress will look for test files
    specPattern: 'cypress/e2e/**/*.{js,jsx}',
    // The base URL for your app
    baseUrl: 'http://localhost:3000',
    // Folder where Cypress will store test artifacts (videos, screenshots, etc.)
    videosFolder: 'cypress/videos',
    screenshotsFolder: 'cypress/screenshots',
    // Folder where Cypress will store fixtures (static data for tests)
    fixturesFolder: 'cypress/fixtures',
    // Folder where Cypress will store test support files
    supportFile: 'cypress/support/index.js',
  },
  // Additional configuration options
  viewportWidth: 1280,
  viewportHeight: 720,
  video: true, // Enable video recording
  retries: {
    runMode: 2, // Retry failed tests in run mode up to 2 times
    openMode: 0, // No retries in interactive mode
  },
});
EOF
```





