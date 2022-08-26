# Contributing Guide

This document aims to describe the workflows and rules used for developing this
project. This includes, but is not limited to:

- how to contribute code (coding standards, testing, documenting source code)
- how pull requests are handled
- how to file bug reports

## Getting Started

Follow the steps below to setup your local development environment:

1. Clone repository

   ```sh
   git clone https://github.com/unicornware/brewfile
   cd brewfile
   ```

2. Set node version

   ```sh
   nvm use
   ```

3. [Configure commit signing][1]

4. Update `~/.gitconfig`

   ```sh
   git config --global commit.gpgsign true
   git config --global user.email <email>
   git config --global user.name <name>
   git config --global user.username <username>
   ```

5. Install dependencies

   ```sh
   yarn
   ```

   **Note**: This project uses [Yarn 2][2]. Consult [`.yarnrc.yml`](.yarnrc.yml)
   for an overview of configuration options and required environment variables.
   Furthermore, if you already have a global Yarn configuration, or any `YARN_*`
   environment variables set, an error will be thrown if any settings conflict
   with the project's Yarn configuration, or the Yarn 2 API. Missing environment
   variables will also yield an error.

6. Update startup file (e.g. `$ZDOTDIR/.zprofile`, `~/.bash_profile`, etc):

   ```sh
   # PATH
   # 1. local node_modules
   [ -d $PWD/node_modules/.bin ] && export PATH=$PWD/node_modules/.bin:$PATH

   # NVM
   # - https://github.com/nvm-sh/nvm
   export NVM_DIR=$HOME/.nvm
   ```

7. Reload shell

   ```sh
   exec $SHELL
   ```

### Environment Variables

#### GitHub Actions

Variables are prefixed by `secrets.` in [workflow](.github/workflows/) files.

### Git Config

The examples in this guide contain references to custom Git aliases.

See [`.github/.gitconfig`](.github/.gitconfig) for an exhaustive list.

## Contributing Code

[Husky][3] is used to locally enforce coding and commit message standards.

Any code merged into the [trunk](#branching-model) must confront the following
criteria:

- changes should be discussed prior to implementation
- changes have been tested properly
- changes should include documentation updates if applicable
- changes have an associated ticket and pull request

### Branching Model

This project follows a [Trunk Based Development][4] workflow, specifically the
[short-lived branch style][5].

- Trunk Branch: `main`
- Short-Lived Branches: `feat/*`, `hotfix/*`, `release/*`

#### Branch Naming Conventions

When creating a new branch, the name should match the following format:

```zsh
[prefix]/<issue-number>-<branch_name>
 │        │              │
 │        │              │
 │        │              │
 │        │              └─⫸ a short, memorable name
 │        │
 │        └─⫸ check github issue
 │
 └─⫸ feat|feat/fix|hotfix|release
```

### Commit Messages

This project follows [Conventional Commit][6] standards and uses [commitlint][7]
to enforce those standards.

This means every commit must conform to the following format:

```zsh
<type>[scope][!]: <description>
 │     │      │    │
 │     │      │    │
 │     │      │    └─⫸ summary in present tense (lowercase without punctuation)
 │     │      │
 │     │      └─⫸ optional breaking change flag
 │     │
 │     └─⫸ see commitlintrc.json
 │
 └─⫸ build|ci|chore|docs|feat|fix|perf|refactor|revert|style|test|wip

[body]

[BREAKING CHANGE: <change>]

[footer(s)]
```

`<type>` must be one of the following values:

- `build`: Changes that affect the build system or external dependencies
- `ci`: Changes to CI/CD configuration files and scripts
- `chore`: Housekeeping tasks / changes that don't impact external users
- `docs`: Documentation improvements
- `feat`: New features
- `fix`: Bug fixes
- `perf`: Performance improvements
- `refactor`: Code improvements
- `revert`: Revert past changes
- `style`: Changes that do not affect the meaning of the code
- `test`: Change that impact the test suite
- `wip`: Working on changes, but you need to go to bed :wink:

e.g:

- `build(deps-dev): bump cspell from 6.7.0 to 6.8.0`
- `perf: lighten initial load`

See [`.commitlintrc.json`](.commitlintrc.json) to view all commit guidelines.

### Code Style

[Prettier][8] is used to format code and [ESLint][9] to lint files.

#### ESLint Configuration

- [`.eslintrc.json`](.eslintrc.json)
- [`.eslintignore`](.eslintignore)

#### Prettier Configuration

- [`.prettierrc.json`](.prettierrc.json)
- [`.prettierignore`](.prettierignore)

### Making Changes

**TODO**: Update documentation.

### Getting Help

If you need help, [start a discussion in the Q&A category][10].

## Labels

This project uses a well-defined list of labels to organize issues and pull
requests. Most labels are scoped (i.e: `status:`).

A list of labels can be found in [`.github/labels.yml`](.github/labels.yml).

## Opening Issues

Before opening an issue, make sure you have:

- read the documentation
- checked that the issue hasn't already been filed by searching open issues
- searched closed issues for solution(s) or feedback

If you haven't found a related open issue, or feel that a closed issue should be
re-visited, open a new issue.

A well-written issue

- contains a well-written summary of the bug, feature, or improvement
- contains a [minimal, reproducible example][11] (if applicable)
- includes links to related articles and documentation (if any)
- includes an emoji in the title :wink:

## Pull Requests

When you're ready to submit your changes, open a pull request (PR) against
`main`:

```sh
https://github.com/unicornware/brewfile/compare/main...$branch
```

where `$branch` is the name of the branch you'd like to merge into `main`.

All PRs are subject to review before being merged into `main`.

Before submitting a PR, be sure you have:

- performed a self-review of your changes
- added and/or updated relevant tests
- added and/or updated relevant documentation

Every PR you open should:

- [follow this template](.github/PULL_REQUEST_TEMPLATE.md)
- [be titled appropriately](#pull-request-titles)

### Pull Request Titles

To keep in line with [commit message standards](#commit-messages) after PRs are
merged, PR titles are expected to adhere to the same rules.

## Merge Strategies

In every repository, the `rebase and merge` and `squash and merge` options are
enabled.

- **rebase and merge**: PR has one commit or commits that are not grouped
- **squash and merge**: PR has one commit or a group of commits

When squashing, be sure to follow [commit message standards](#commit-messages):

```zsh
<type>[scope][!]:<pull-request-title> (#pull-request-n)
 │     │      │   │                    │
 │     │      │   │                    │
 │     │      │   │                    └─⫸ check pull request
 │     │      │   │
 │     │      │   └─⫸ lowercase title
 │     │      │
 │     │      └─⫸ optional breaking change flag
 │     │
 │     └─⫸ see .commitlintrc.json
 │
 └─⫸ build|ci|chore|docs|feat|fix|perf|refactor|release|revert|style|test
```

e.g:

- `ci(workflows): simplify release workflow #24`
- `refactor: project architecture #21`

[1]:
  https://docs.github.com/authentication/managing-commit-signature-verification/about-commit-signature-verification#gpg-commit-signature-verification
[2]: https://yarnpkg.com/getting-started
[3]: https://github.com/typicode/husky
[4]: https://trunkbaseddevelopment.com
[5]: https://trunkbaseddevelopment.com/styles/#short-lived-feature-branches
[6]: https://conventionalcommits.org
[7]: https://github.com/conventional-changelog/commitlint
[8]: https://prettier.io
[9]: https://eslint.org
[10]: https://github.com/unicornware/brewfile/discussions/new?category=q-a
[11]: https://stackoverflow.com/help/minimal-reproducible-example
