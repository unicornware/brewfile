# Contributing Guide

## Overview

[Getting Started](#getting-started)\
[Contributing Code](#contributing-code)\
[Labels](#labels)\
[Opening Issues](#opening-issues)\
[Pull Requests](#pull-requests)

## Getting Started

### Git Configuration

The examples in this guide contain references to custom Git aliases.

See [`.gitconfig`](.github/.gitconfig) for an exhausive list of aliases.

### Clone & Install

```zsh
git clone https://github.com/unicornware/brewfile ~/.config/brewfile
cd ~/.config/brewfile
```

## Contributing Code

[Husky][1] is used to run both Git hooks that locally enforce coding and commit
message standards, as well as test suites.

### Commit Messages

This project follows [Conventional Commit][2] standards and uses [commitlint][3]
to enforce those standards.

This means every commit must conform to the following format:

```zsh
<type>[optional scope]: <description>
 │     │                │
 │     │                └─⫸ summary in present tense; lowercase without period at the end
 │     │
 │     └─⫸ see .commitlintrc.ts
 │
 └─⫸ build|ci|chore|docs|feat|fix|perf|refactor|revert|style|test|wip

[optional body]

[optional footer(s)]
```

`<type>` must be one of the following values:

- `build`: Changes that affect the build system or external dependencies
- `ci`: Changes to our CI configuration files and scripts
- `chore`: Changes that don't impact external users
- `docs`: Documentation only changes
- `feat`: New features
- `fix`: Bug fixes
- `perf`: Performance improvements
- `refactor`: Code improvements
- `revert`: Revert past changes
- `style`: Changes that do not affect the meaning of the code
- `test`: Adding missing tests or correcting existing tests
- `wip`: Working on changes, but you need to go to bed :wink:

e.g:

- `git ac 'docs(brew): add comments'` -> `docs(brew): add comments`

See [`.commitlintrc.json`](.commitlintrc.json) for an exhasutive list of valid
commit scopes and types.

### Making Changes

**TODO**: Update documentation.

## Labels

This project uses a well-defined list of labels to organize tickets and pull
requests. Most labels are grouped into different categories (identified by the
prefix, eg: `status:`).

A list of labels can be found in [`.github/labels.yml`](.github/labels.yml).

## Opening Issues

Before opening an issue please make sure, you have:

- read the documentation
- searched open issues for an existing issue with the same topic
- search closed issues for a solution or feedback

If you haven't found a related open issue, or feel that a closed issue should be
re-visited, please open a new issue. A well-written issue has the following
traits:

- follows an [issue template](.github/ISSUE_TEMPLATE)
- is [labeled](#labels) appropriately
- contains a well-written summary of the feature, bug, or problem statement
- contains a minimal, inlined code example (if applicable)
- includes links to prior discussions and resources (if you've found any)

## Pull Requests

When you're ready to have your changes reviewed, open a pull request against the
`next` branch.

Every opened PR should:

- use [**this template**](.github/PULL_REQUEST_TEMPLATE.md)
- reference it's ticket id
- be [labeled](#labels) appropriately
- be assigned to yourself
- give maintainers push access so quick fixes can be pushed to your branch

### Pull Request URL Format

```zsh
https://github.com/unicornware/brewfile/compare/next...<branch>
```

where `<branch>` is the name of the branch you'd like to merge into `next`.

[1]: https://github.com/typicode/husky
[2]: https://conventionalcommits.org
[3]: https://github.com/conventional-changelog/commitlint
