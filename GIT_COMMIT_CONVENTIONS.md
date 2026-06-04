# Git Commit Message Conventions

This document outlines the commit message standards that all developers should follow in this repository. These conventions ensure a clean, readable git history and facilitate better collaboration, debugging, and automation.

## Table of Contents

- [Format Structure](#format-structure)
- [Commit Types](#commit-types)
- [Scope](#scope)
- [Subject Line](#subject-line)
- [Body](#body)
- [Footer](#footer)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Tools & Automation](#tools--automation)

---

## Format Structure

All commits should follow this format:

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Rules:**
- The header (first line) is mandatory
- The body and footer are optional but recommended for complex changes
- Separate the header from the body with a blank line
- Separate the body from the footer with a blank line
- All lines must be wrapped at 72 characters (except URLs)

---

## Commit Types

Use one of the following types to categorize your commit:

| Type | Purpose | Example |
|------|---------|---------|
| **feat** | A new feature | `feat(auth): add two-factor authentication` |
| **fix** | A bug fix | `fix(database): resolve connection timeout` |
| **docs** | Documentation changes | `docs(README): update setup instructions` |
| **style** | Code style changes (formatting, semicolons, etc.) | `style(linter): fix eslint violations` |
| **refactor** | Code refactoring without changing functionality | `refactor(utils): simplify error handling` |
| **perf** | Performance improvements | `perf(api): optimize query caching` |
| **test** | Adding or updating tests | `test(auth): add login validation tests` |
| **chore** | Build process, dependencies, tooling | `chore(deps): update npm packages` |
| **ci** | CI/CD configuration changes | `ci: add GitHub Actions workflow` |

---

## Scope

The scope specifies which part of the codebase is affected. It should be concise and descriptive.

**Common scopes in this repository:**
- `makefile` - Makefile changes
- `shell` - Shell scripts
- `javascript` - JavaScript files
- `build` - Build process
- `scripts` - Script utilities
- `config` - Configuration files
- `docs` - Documentation

**Scope is optional** but highly recommended for clarity.

### Scope Examples:
```
feat(makefile): add deployment target
fix(shell): correct script permissions
docs(javascript): add utility function docs
refactor(scripts): improve error handling
```

---

## Subject Line

The subject is a concise description of the change.

### Rules:
- ✅ **Use imperative mood**: "add", "fix", "remove" (not "added", "fixed", "removed")
- ✅ **Lowercase**: Start with lowercase letter
- ✅ **No period**: Do not end with a period or punctuation
- ✅ **Concise**: Maximum 50 characters
- ✅ **Specific**: Describe what changed, not why

### Good Examples:
```
feat(makefile): add test automation target
fix(shell): correct file path resolution
refactor(javascript): improve error handling
docs(scripts): add usage instructions
style(code): fix indentation inconsistencies
test(build): add makefile validation tests
```

### Bad Examples:
```
❌ Fixed bugs in the script
❌ Updated stuff
❌ feat(makefile): This commit adds a new feature to the Makefile...
❌ wip: working on stuff
❌ Fix.
```

---

## Body

The body explains **what** and **why**, not **how**. It should provide context for the change.

### Rules:
- Wrap at 72 characters
- Separate from subject with a blank line
- Explain the problem and solution
- Use bullet points for multiple changes
- Reference related issues or PRs

### Body Examples:

**Makefile feature:**
```
feat(makefile): add Docker build and push targets

Add convenient make targets for building and pushing Docker images
to the registry. This streamlines the containerization workflow.

Changes:
- Add build target for Docker image compilation
- Add push target for registry uploads
- Include environment variable support
```

**Shell script fix:**
```
fix(shell): correct path resolution in deploy script

The script was using relative paths that failed when invoked from
different directories. Changed to use absolute paths based on script
location.
```

**JavaScript refactoring:**
```
refactor(javascript): extract utility functions into modules

Move repeated utility code into separate, reusable modules to:
- Improve code maintainability
- Enable better unit testing
- Reduce code duplication
```

---

## Footer

The footer is used for metadata and references. Common footer types:

### Closes/Fixes Issues:
```
Closes #123
Closes #456, #789
Fixes #1000
```

### Breaking Changes:
```
BREAKING CHANGE: removed Node 10 support

The application now requires Node 12 or higher.
Update your environment accordingly.
```

### Co-authors:
```
Co-authored-by: Jane Doe <jane@example.com>
Co-authored-by: John Smith <john@example.com>
```

### Custom Trailers:
```
Reviewed-by: Lead Developer <lead@example.com>
Depends-on: #555
Related-to: #666
```

---

## Examples

### Complete Feature Commit

```
feat(makefile): add comprehensive build automation

Add new make targets to automate the complete build, test, and deploy
workflow. Supports multiple environments and configurations.

Changes:
- Add build target with optimization flags
- Add test target with coverage reporting
- Add deploy target with safety checks
- Add clean target for artifact removal

This streamlines the development workflow and reduces manual build
steps.

Closes #234
Reviewed-by: Lead Developer <lead@example.com>
```

### Bug Fix Commit

```
fix(shell): resolve permission denied errors in deploy script

The deploy script lacked execute permissions when pulled from the
repository. Added chmod command in post-checkout hook and updated
documentation.

Fixes #567
```

### Documentation Commit

```
docs(scripts): add comprehensive usage guide

Add detailed documentation for all available scripts including:
- Purpose and usage of each script
- Required environment variables
- Common error troubleshooting
- Examples for each use case

- Document setup.sh
- Document deploy.sh
- Document build.sh
- Add troubleshooting section
```

### Refactoring Commit

```
refactor(javascript): consolidate utility functions

Extract repeated utility code from multiple files into a dedicated
utils module. This reduces duplication and improves maintainability.

No functional changes - all tests pass.
```

### Chore Commit

```
chore(deps): update Node.js to v18.0.0

Update project dependencies:
- Node.js: 16.13.0 → 18.0.0
- ESLint: 7.x → 8.x
- Prettier: 2.x → 3.x

All tests passing. No breaking changes.
```

---

## Best Practices

### ✅ DO:

1. **Write atomic commits**: Each commit should represent one logical change
   ```
   Good: One commit for adding feature, another for tests
   Bad: Everything in a single "fixed stuff" commit
   ```

2. **Commit frequently**: Small, focused commits are easier to review and debug
   ```
   Good: 10 focused commits
   Bad: 1 massive commit with 50 files changed
   ```

3. **Test before committing**: Ensure all tests pass before making a commit
   ```bash
   make test
   git commit -m "feat(feature): add new functionality"
   ```

4. **Use imperative mood**: Pretend your commit completes this sentence: "If applied, this commit will _____"
   ```
   Good: "add user authentication"
   Bad: "added user authentication" or "adds user authentication"
   ```

5. **Review your commit**: Use `git diff` to review changes before committing
   ```bash
   git diff --cached
   git commit
   ```

6. **Use git hooks**: Set up pre-commit hooks to validate commit messages
   ```bash
   # Install commitlint to enforce message format
   npm install --save-dev @commitlint/cli @commitlint/config-conventional
   ```

### ❌ DON'T:

1. **Don't mix multiple concerns**: Keep commits focused and logical
   ```
   Bad: "fix: multiple bug fixes and improvements"
   Good: Separate commits for each fix
   ```

2. **Don't use generic messages**: Be specific and descriptive
   ```
   Bad: "fix", "wip", "stuff", "things"
   Good: "fix(makefile): resolve build target issue"
   ```

3. **Don't commit sensitive information**: Never commit passwords, API keys, or personal data
   ```bash
   # Use .gitignore for sensitive files
   echo ".env.local" >> .gitignore
   ```

4. **Don't rewrite published history**: Avoid force pushing to shared branches
   ```bash
   # Avoid on main/develop/shared branches
   git push --force  # ❌ DON'T DO THIS
   
   # OK for feature branches
   git push --force-with-lease origin feature-branch  # ✅ OK
   ```

5. **Don't commit incomplete work**: Ensure code is tested and working
   ```
   Bad: "wip: half-finished build script"
   Good: Complete, tested feature
   ```

---

## Tools & Automation

### Commitlint

Automatically validate commit messages against these conventions:

```bash
# Installation
npm install --save-dev @commitlint/cli @commitlint/config-conventional

# Create commitlint.config.js
echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js

# Create .husky/commit-msg hook
npx husky add .husky/commit-msg 'npx --no -- commitlint --edit "$1"'
```

### Husky + Git Hooks

Automate linting and testing before commits:

```bash
# Installation
npm install --save-dev husky
npx husky install

# Add pre-commit hook
npx husky add .husky/pre-commit 'make test'
```

### Conventional Commits Standard

This repository follows the [Conventional Commits](https://www.conventionalcommits.org/) specification, which enables:

- **Automatic changelog generation**
- **Semantic versioning (semver)**
- **Better commit history analysis**

### Interactive Rebase

Clean up commits before pushing:

```bash
# Rebase last 3 commits
git rebase -i HEAD~3

# In the editor:
# pick = use commit
# reword = use commit, but edit the commit message
# squash = use commit, but meld into previous commit
# fixup = like squash, but discard log message
```

### Amend Last Commit

Fix your most recent commit:

```bash
# Add changes to the commit
git add .
git commit --amend --no-edit

# Or edit the commit message
git commit --amend -m "feat(makefile): corrected message"
```

### Viewing Commit History

```bash
# View formatted log
git log --oneline --graph --all

# View specific author's commits
git log --author="Name" --oneline

# View commits for a specific file
git log --follow -p -- path/to/Makefile

# View commits with filtering
git log --grep="fix" --oneline
```

---

## Repository Information

**Repository:** sohag47/Dev-Pro  
**Description:** All type of commends  
**Primary Languages:**
- Makefile (44.4%)
- Shell (31.8%)
- JavaScript (23.8%)

This documentation applies to all commits across all language components.

---

## Questions?

If you have questions about these conventions, please refer to:

- [Conventional Commits](https://www.conventionalcommits.org/)
- [Angular Commit Guidelines](https://github.com/angular/angular/blob/master/CONTRIBUTING.md#commit)
- [Git Documentation](https://git-scm.com/docs)

---

**Last Updated:** June 2026  
**Version:** 1.0
