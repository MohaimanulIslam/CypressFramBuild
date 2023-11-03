# CypressGrip
**To Install Grip**

#using NPM
#To Install Grip
npm i -D @cypress/grep
#using Yarn
yarn add -D @cypress/grep

// cypress/support/index.js or e2e.js
// load and register the grep feature using "require" function
// https://github.com/cypress-io/cypress/tree/develop/npm/grep
const registerCypressGrep = require('@cypress/grep')
registerCypressGrep()

// if you want to use the "import" keyword
// note: `./index.d.ts` currently extends the global Cypress types and
// does not define `registerCypressGrep` so the import path is directly
// pointed to the `support.js` file
import registerCypressGrep from '@cypress/grep/src/support'
registerCypressGrep()


// "import" with `@ts-ignore`
// @see error 2306 https://github.com/microsoft/TypeScript/blob/3fcd1b51a1e6b16d007b368229af03455c7d5794/src/compiler/diagnosticMessages.json#L1635
// @ts-ignore
import registerCypressGrep from '@cypress/grep'
registerCypressGrep()

// cypress.config.js
{
  e2e: {
    setupNodeEvents(on, config) {
      require('@cypress/grep/src/plugin')(config);
      return config;
    },
  }
}

#run only the tests with "auth user" in the title
$ npx cypress run --env grep="auth user"
#run tests with "hello" or "auth user" in their titles
#by separating them with ";" character
$ npx cypress run --env grep="hello; auth user"
#run tests tagged @fast
$ npx cypress run --env grepTags=@fast
#run only the tests tagged "smoke"
#that have "login" in their titles
$ npx cypress run --env grep=login,grepTags=smoke
#only run the specs that have any tests with "user" in their titles
$ npx cypress run --env grep=user,grepFilterSpecs=true
#only run the specs that have any tests tagged "@smoke"
$ npx cypress run --env grepTags=@smoke,grepFilterSpecs=true
#run only tests that do not have any tags
#and are not inside suites that have any tags
$ npx cypress run --env grepUntagged=true
