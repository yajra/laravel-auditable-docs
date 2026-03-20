---
title: "Contributing"
description: "Guidelines for contributing to Laravel Auditable."
---

# Contributing

Contributions are **welcome** and will be fully **credited**.

We accept contributions via Pull Requests on [GitHub](https://github.com/yajra/laravel-auditable).

<a name="pull-requests"></a>
## Pull Requests

- **[PSR-2 Coding Standard](https://www.php-fig.org/psr/psr-2/)** - The easiest way to apply the conventions is to install [PHP Code Sniffer](https://pear.php.net/package/PHP_CodeSniffer/).

- **Document any change in behaviour** - Make sure the `README.md` and any other relevant documentation are kept up-to-date.

- **Consider our release cycle** - We try to follow [SemVer v2.0.0](https://semver.org/). Randomly breaking public APIs is not an option.

- **Send coherent history** - Make sure each individual commit in your pull request is meaningful. If you had to make multiple intermediate commits while developing, please squash them before submitting.

- **Run tests** - Ensure all tests pass before submitting a pull request.

```bash
./vendor/bin/phpunit
```

- **Type check** - Run static analysis to catch type errors:

```bash
./vendor/bin/phpstan analyse
```

<a name="coding-standards"></a>
## Coding Standards

This project uses [Pint](https://laravel.com/docs/11.x/pint) for code style enforcement:

```bash
./vendor/bin/pint
```

<a name="commit-messages"></a>
## Commit Messages

This project follows the [Conventional Commits](https://www.conventionalcommits.org/) specification. All commit messages must follow this format:

```
<type>: <description>
```

**Allowed types:**

| Type | Description |
|------|-------------|
| `feat` | A new feature |
| `fix` | A bug fix |
| `docs` | Documentation only changes |
| `refactor` | Code change that neither fixes a bug nor adds a feature |
| `test` | Adding or correcting tests |
| `chore` | Maintenance tasks (dependencies, config, etc.) |

**Examples:**

```bash
feat: add support for custom created by column
fix: resolve attribute casting issue
docs: update README with new examples
refactor: extract auditor service class
test: add unit tests for auditable trait
chore: update dependencies
```

> **Note:** Pull requests with non-conventional commit messages may be rejected. Please ensure your commits follow this format before submitting.

<a name="bug-reports"></a>
## Bug Reports

When filing a bug report, please include:

- A clear description of the problem
- Steps to reproduce the issue
- Expected behavior vs actual behavior
- Laravel and PHP versions
- Any relevant error messages or stack traces

<a name="feature-requests"></a>
## Feature Requests

Feature requests are welcome. Please describe:

- The problem you're trying to solve
- How you envision the solution
- Any alternative solutions you've considered

**Happy coding!**
