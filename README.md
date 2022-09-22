![Security Checks](https://github.com/pairing4good/react-18-project-template/actions/workflows/codeql-analysis.yml/badge.svg)

![Test Automation](https://github.com/pairing4good/react-18-project-template/actions/workflows/node.js.yml/badge.svg)

## Approach

This starter template standardizes coding standards, industry best practices and detects security vulnerabilities before code is committed to git. This provides fast automated testing feedback loops so teams can focus on solving problems.

### Code Analysis

This template uses [ESLint](https://eslint.org/) to analyze the code in this repository. [ESLint](https://eslint.org/) is configured in `.eslintrc.json` file at the root of the repository. This template leverages 6 plugins that provide fast feedback on coding best practices and common pitfalls.

1. The default coding style guide was adopted from [Airbnb](https://github.com/airbnb/javascript)
2. [eslint-plugin-react](https://github.com/jsx-eslint/eslint-plugin-react)
3. [eslint-plugin-react-hooks](https://www.npmjs.com/package/eslint-plugin-react-hooks)
4. [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier)
5. [eslint-plugin-promise](https://github.com/xjamundx/eslint-plugin-promise)
6. [eslint-plugin-jest](https://github.com/jest-community/eslint-plugin-jest)

At the bottom of the `.eslintrc.json` file `"react/react-in-jsx-scope": "off"` is added to the `rules` section. This linting rule was disabled because it is no longer accurate starting in [React v17](https://reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html).

To run [ESLint](https://eslint.org/) run the command `npm run lint`. [ESLint](https://eslint.org/) can automatically fix problems by running `npm run lint:fix`.

If you are using [VSCode](https://code.visualstudio.com/) adding the ESLint (dbaeumer.vscode-eslint) plugin provides live feedback as you are writing code.  Faster feedback loops help team members learn team style guidelines faster and avoid delays while committing.

### Credentials Check

It's all too common for developers to accidentally commit usernames and or passwords int their repository. This can lead to significant security vulnerabilities and even lead to security breaches. [Secretlint](https://github.com/secretlint/secretlint) is a Pluggable linting tool that prevents developers from committing their credentials. [Secretlint](https://github.com/secretlint/secretlint) is configured in the `.secretlintrc.json` file at the root of this repository.

To run [Secretlint](https://github.com/secretlint/secretlint) run the command `npm run secretlint`.

### NPM Package Audit

The `npm audit` command checks the dependencies configured in `package.json` for vulnerabilities. In rare circumstances some vulnerability need to be temporarily ignored while the open source library community works on a fix. Unfortunately `npm audit` does not provide this ability. However, the [better-npm-audit](https://github.com/jeemok/better-npm-audit) library does. The `.nsprc` file at the root of this repository configures temporary exceptions. If this need arises be sure to the [expiry](https://github.com/jeemok/better-npm-audit#using-nsprc-file-to-manage-exceptions) field to set a date when this vulnerability will be reevaluated by your team. **_ Avoid ignoring audit level [critical](https://docs.npmjs.com/cli/v8/commands/npm-audit#audit-level). These vulnerabilities should be addressed immediately. _**

### Reformatting Code

[ESLint](https://eslint.org/)'s auto fix command reformats your files to fit the configured [ESLint](https://eslint.org/) rules. Beyond linting [Prettier](https://prettier.io/) provides configurable coding styles. [Prettier](https://prettier.io/) rules are configured in the `.prettierrc` file at the root of this repository. By running the command `npm run lint:fix` the [Prettier](https://prettier.io/) rules will be included in the [ESLint](https://eslint.org/) formatting rules. It's important that teams have clear coding standards and libraries like [Prettier](https://prettier.io/) can help teams configure and adhere to their own standards.

## Code Coverage

Test automation is essential for longterm product health. Each test exercises the application and ensures that it behaves the way that the customer expects. As products grow it's not uncommon to have tens of thousands of [unit tests](https://martinfowler.com/bliki/UnitTest.html) that run in a few milliseconds. Beyond [unit tests](https://martinfowler.com/bliki/UnitTest.html) teams invest in [integration tests](https://martinfowler.com/bliki/IntegrationTest.html) and [user interface testing](https://martinfowler.com/bliki/TestPyramid.html). Teams that are committed to [test driving](https://en.wikipedia.org/wiki/Test-driven_development) code often write thoughtful tests that provide comprehensive product test coverage.

Code coverage verification can be usful for teams to identify test coverage holes within their product. These thresholds simply identify if a line of code was exercised by a test. However, it cannot determine if the test coverage ise exercising the code in a meaningful way. Code coverage thresholds only identify test coverage gaps and should not be used as a substitute for a strong team culture of technical excellence.

This repository uses the [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/). By default [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/) is configured to use [Jest](https://jestjs.io/) under the hood. Within [Jest](https://jestjs.io/) [test coverage thresholds](https://jestjs.io/docs/configuration#coveragethreshold-object) are set in the `jest.config.js` file at the root of this repository.

### Checks Before Committing

This template uses [Husky](https://typicode.github.io/husky) to verify the code before it is commited to [git](https://git-scm.com/). The `.husky/pre-commit` file is run before a `git commit` is completed. This file configures and runs coding style, test coverage, and security check verifications prior to commiting code to git.

In [git](https://git-scm.com/) only commits [staged](https://githowto.com/staging_and_committing) files. If [Husky](https://typicode.github.io/husky) reformatted all files whether they are [staged](https://githowto.com/staging_and_committing) or not, it would frequently change files that were not [staged](https://githowto.com/staging_and_committing) and would not be ultimatley committed. To solve this problem, [Husky](https://typicode.github.io/husky) uses the [lint-staged](https://github.com/okonet/lint-staged) library to only run formatting rules against staged files. The commands that are run with [lint-staged](https://github.com/okonet/lint-staged) library are configured in the `.lintstagedrc.json` file at the root of this repository.

To run [lint-staged](https://github.com/okonet/lint-staged) run the command `npm run lint-staged`.

Before each commit [Husky](https://typicode.github.io/husky) runs 5 commands:

1. `npm run lint-staged` - automatically fixes as many linting rules as resolved and reformatts files with Prettier
2. `npm run test:coverage` - runs all the tests and checks the coverage threshold
3. `npm run lint` - checks the code against all of the linting rules
4. `npm run secretlint` - checks for secrets within the code
5. `npm run audit` - checks for package vulnerabilites

# Initial Template Creation Steps

## Install NVM

https://github.com/nvm-sh/nvm

curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

## Install Node

nvm install node

## Create React App

npx create-react-app tdd-amplify-react

## Set Up ESLint

https://dev.to/knowankit/setup-eslint-and-prettier-in-react-app-357b

- npm install eslint --save-dev
- npx eslint --init

- ✔ How would you like to use ESLint? · style
- ✔ What type of modules does your project use? · esm
- ✔ Which framework does your project use? · react
- ✔ Does your project use TypeScript? · No
- ✔ Where does your code run? · browser
- ✔ How would you like to define a style for your project? · guide
- ✔ Which style guide do you want to follow? · airbnb
- ✔ What format do you want your config file to be in? · JSON
- ✔ Would you like to install them now? · Yes
- ✔ Which package manager do you want to use? · npm

## Set Up Linting Rules

- npm install eslint-config-prettier eslint-plugin-prettier prettier --save-dev
- npm install eslint-plugin-promise --save-dev
- npm install eslint-plugin-jest --save-dev
- npm install eslint-plugin-react-hooks --save-dev

## Prevent committing credential

- npm install secretlint @secretlint/secretlint-rule-preset-recommend --save-dev
- npx secretlint --init
