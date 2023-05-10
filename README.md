# probando-emojis
# Unicomer Workflow Frontend

[![Quality gate](http://34.139.112.156:9000/api/project_badges/quality_gate?project=unicomer-workflow-frontend&token=e8a55819bb8c72c6865af4e0479d170384ac4ebf)](http://34.139.112.156:9000/dashboard?id=unicomer-workflow-frontend)

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 13.1.2.

## Table of Contents

1. [Quick Start](#1-quick-start)
2. [Dependencies](#2-dependencies)
3. [Environments](#3-environments)
4. [Branches](#4-branches)
5. [Versioning](#5-versioning)
6. [Development Flow](#6-development-flow)
7. [Bugfix Flow](#7-bugfix-flow)
8. [Testing](#8-testing)

## 1. Quick Start

Clone the repository with the URL provided by GitLab. Use of SSH is recommended for security standard.

```sh
git clone <REPO_URL>
```

Install the version of NodeJS and NPM configured in the `.nvmrc` file. [More info about NVM usage](https://github.com/nvm-sh/nvm).

```sh
nvm use
```

If the version is not installed, you need to run

```sh
nvm install <VERSION>
```

Now you are ready to run

```sh
npm install
```

[&uarr; Back to top](#unicomer-workflow-frontend)

## 2. Dependencies

- `angular/material` for UI components and design style guidance. Customs color scheme was added in `src/scss/_theming.scss`.

- `ngx-translate` for i18n. The default app language is in English but supports other available languages in `src/assets/i18n`.

- `keycloak-angular` for client-side authentication and authorization management that is extended in the project with the `AuthService` (`src/app/core/services/auth.service.ts`).

- `angular-eslint` & `prettier` for consistent code style, formatting and static analysis. The configuration files are `.eslintrc.json` and `.prettierrc.json` in root respectively.

- `husky` for git hooks integration. There are two actions configured in the project:

  1. `Pre-commit` (`.husky/pre-commit`) to format staged code and run ESLint before commit the code.
  2. `Pre-push` (`.husky/pre-push`) to run tests before push the code.

[&uarr; Back to top](#unicomer-workflow-frontend)

## 3. Environments

There are 5 different environments:

**Local (LOCAL)** uses `/src/environments/environment.ts` file.

- This is the suggested environment for developing features and bug fixes locally.
- Default to **`ng serve`**.
- Configuration alias is `--configuration=local`.

**Development (DEV)** uses `/src/environments/environment.dev.ts` file.

- This environment is for deploying the application with development URL.
- LOCAL URL and DEV URL are the same.
- Configuration alias is `--configuration=development`.
- NPM build script for CI/CD is `npm run build:dev`.

**Quality Assurance (QA)** uses `/src/environments/environment.qa.ts` file.

- This environment is for deploying the application with QA URL.
- It's mainly used for testing by QA team.
- Configuration alias is `--configuration=qa`.
- NPM build script for CI/CD is `npm run build:qa`.

**User acceptance testing (UAT)** uses `/src/environments/environment.qa.ts` file.

- This environment is for deploying the application with UAT URL.
- It's mainly used for testing by QA team, with the difference that the data is similar to production.
- Configuration alias is `--configuration=uat`.
- NPM build script for CI/CD is `npm run build:qa`.

**Production (PROD)** uses `/src/environments/environment.prod.ts` file.

- This environment is for deploying the application with production URL.
- Default to **`ng build`** (use build script for CI/CD).
- Configuration alias is `--configuration=production`.
- NPM build script for CI/CD is `npm run build:prod` (recommended).

[&uarr; Back to top](#unicomer-workflow-frontend)

## 4. Branches

| Branch | Environment |
| :----: | :---------: |
| `main` |    PROD     |
| `uat`  |     UAT     |
|  `qa`  |     QA      |
| `dev`  |     DEV     |

[&uarr; Back to top](#unicomer-workflow-frontend)

## 5. Versioning

To track the version of the application, the `version` file in the root is used. Given a version number MAJOR.MINOR.PATCH, increment the:

1. MAJOR version when the app accumulates significant changes in production.
2. MINOR version when starting a new sprint. This number must match the sprint number.
3. PATCH version when you merge a feature/bugfix branch into a [default branch](#branches).

[&uarr; Back to top](#unicomer-workflow-frontend)

## 6. Development Flow

As a standard, all application development must be written in English, including GIT commit messages and the code itself. Internationalization assets are excluded from this consideration.

It is recommended to use [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) and its [VSCode extension](https://marketplace.visualstudio.com/items?itemName=vivaxy.vscode-conventional-commits) as well. Use of [gitmoji](https://gitmoji.dev/) is allowed.

For reference of backend's endpoints you can go to the [Swagger](https://credits-api-dev.unicomer.com/credits-workflow-backend-dev/swagger-ui/index.html) resource and enter `/credits-workflow-backend-dev/v3/api-docs` in the search input to get de documentation.

To start the development, you should work in the `dev` branch and pull recent changes. You can then create the feature branch with the suggested name `WMA-<US_NUMBER>`, example:

```shh
git checkout dev
git pull origin
git checkout -b WMA-1234
```

When the feature is ready, push the changes to the repository and create a merge request that includes the branch name in the title and points to the `dev` branch. When this is approved, you can merge with `dev` and then merge `dev` with `qa` for QA review.

> Note: Don't forget to update de `version` file to reflect deployment in the respective environments.

[&uarr; Back to top](#unicomer-workflow-frontend)

## 7. Bugfix Flow

To make a bugfix required in QA, follow de [Development Flow](#6-development-flow).

Otherwise, if bugfix is required in UAT/PROD, you should move to the `uat` branch and pull recent changes. You can then create the feature branch with the suggested name `bugfix/WMA-<US_NUMBER>`, example:

```shh
git checkout uat
git pull origin
git checkout -b bugfix/WMA-1234
```

When the bugfix is ready, push the changes to the repository and create a merge request that includes the branch name in the title and points to the `uat` branch update the `version` file with respect the latest value in the `uat` branch. When this is approved, you can merge with `uat` without delete the _bugfix branch_.

Now, move to the _bugfix branch_ and update the `version` file with respect the latest value on the `dev` branch and then merge it with the `dev` branch and the `qa` branch for QA review and sync the changes.

[&uarr; Back to top](#unicomer-workflow-frontend)

## 8. Testing

Run `npm test` to execute the unit tests via [Jest](https://jestjs.io/docs/getting-started).

Run `npm test:watch` to watch files for changes and rerun all tests when something changes.

[&uarr; Back to top](#unicomer-workflow-frontend)
 
 
