# Changelog Conventions Guide

## Overview

A changelog is a curated, chronologically ordered list of notable changes for each version of a project. A good changelog helps users and contributors understand what has changed between releases.

## Why Keep a Changelog?

**For Users**:
- Quickly understand what's new
- Assess upgrade urgency (security fixes vs. features)
- Identify breaking changes before upgrading
- Plan migration efforts

**For Contributors**:
- See project evolution
- Understand what work has been completed
- Avoid duplicate work

**For Maintainers**:
- Track project history
- Generate release notes
- Communicate value to stakeholders

## Guiding Principles

1. **Changelogs are for humans, not machines**
   - Write for your audience, not for scripts
   - Use clear, plain language
   - Avoid jargon when possible

2. **One entry per significant change**
   - Don't list every commit
   - Group related changes
   - Focus on user-facing impact

3. **Keep the latest version at the top**
   - Most recent first
   - Users care most about what's new

4. **Include dates and version numbers**
   - Format: `## [1.2.0] - 2024-01-15`
   - Use ISO 8601 date format (YYYY-MM-DD)

5. **Group changes by category**
   - Makes scanning easier
   - Helps users find relevant information

6. **Link to issues and pull requests**
   - Provides context
   - Credits contributors
   - Enables deeper investigation

## Keep a Changelog Format

Based on [keepachangelog.com](https://keepachangelog.com/), the standard format for changelogs.

### Standard Categories

Use these categories in this order:

#### **Added** (New Features)
New features or functionality added to the project.
- "Added dark mode toggle to settings"
- "Added support for PostgreSQL database"

#### **Changed** (Changes in Existing Functionality)
Changes to existing features, behavior, or functionality.
- "Changed default timeout from 30s to 60s"
- "Updated user profile layout for better usability"

#### **Deprecated** (Soon-to-be Removed Features)
Features that are marked for removal in future versions.
- "Deprecated the `oldMethod()` function, use `newMethod()` instead"
- "Deprecated support for Node.js v14 (EOL in 6 months)"

#### **Removed** (Removed Features)
Features that have been removed in this release.
- "Removed support for Internet Explorer 11"
- "Removed deprecated `getUserInfo()` method"

#### **Fixed** (Bug Fixes)
Bugs that have been fixed.
- "Fixed crash when uploading files larger than 100MB"
- "Fixed incorrect calculation in tax estimator"

#### **Security** (Security Patches)
Vulnerabilities and security improvements (always list these!)
- "Fixed SQL injection vulnerability in search endpoint"
- "Updated bcrypt to v5.1.0 to address CVE-2024-XXXXX"

#### Optional Categories:

**Performance** (Performance Improvements)
- "Improved database query performance by 40%"
- "Reduced initial page load time from 3s to 1.2s"

**Documentation** (Documentation Changes)
- "Added API documentation for authentication endpoints"
- "Updated installation guide for Windows users"

## Changelog Template

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- List of features added but not yet released

### Changed
- List of changes to existing features

## [1.2.0] - 2024-01-15

### Added
- User authentication with OAuth2 support
- Dark mode theme option in settings
- Export data to CSV functionality

### Changed
- Updated dashboard layout for improved usability
- Improved error messages for API validation failures

### Fixed
- Fixed crash when filtering large datasets
- Corrected timezone handling for scheduled tasks

## [1.1.0] - 2024-01-01

### Added
- Multi-language support (English, Spanish, French)
- Email notification preferences

### Fixed
- Fixed memory leak in background task processor

### Security
- Updated dependencies to address CVE-2023-XXXXX

## [1.0.0] - 2023-12-15

### Added
- Initial release
- User registration and login
- Dashboard with key metrics
- Basic reporting functionality

[Unreleased]: https://github.com/user/project/compare/v1.2.0...HEAD
[1.2.0]: https://github.com/user/project/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/user/project/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/user/project/releases/tag/v1.0.0
```

## Conventional Commits

Conventional Commits is a specification for writing standardized commit messages that can be automatically parsed to generate changelogs.

### Format

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Types

**feat**: A new feature (MINOR version bump)
```
feat: add user profile page
feat(api): add endpoint for user preferences
```

**fix**: A bug fix (PATCH version bump)
```
fix: resolve crash on empty input
fix(auth): correct token expiration handling
```

**docs**: Documentation changes only
```
docs: update installation instructions
```

**style**: Code style changes (formatting, whitespace, etc.)
```
style: format code with prettier
```

**refactor**: Code changes that neither fix bugs nor add features
```
refactor: extract validation logic into separate module
```

**perf**: Performance improvements
```
perf: optimize database queries for user dashboard
```

**test**: Adding or updating tests
```
test: add integration tests for payment flow
```

**build**: Changes to build system or dependencies
```
build: upgrade webpack to v5
```

**ci**: Changes to CI/CD configuration
```
ci: add automated security scanning
```

**chore**: Other changes that don't modify src or test files
```
chore: update package.json metadata
```

### Breaking Changes

Indicate breaking changes with `!` after type or with `BREAKING CHANGE:` in footer:

```
feat!: change API response format

BREAKING CHANGE: API now returns JSON object instead of array
```

### Examples

```
feat(auth): add OAuth2 authentication

Adds OAuth2 authentication support for Google and GitHub providers.
Users can now log in using their existing accounts.

Closes #123
```

```
fix(ui): resolve button alignment on mobile

The submit button was misaligned on screens smaller than 768px.
Updated CSS to properly center the button.

Fixes #456
```

## Writing Great Changelog Entries

### Do ✅

**Be clear and concise**
- ✅ "Fixed crash when uploading files over 100MB"
- ❌ "Fixed issue with files"

**Focus on impact, not implementation**
- ✅ "Improved page load time by 50%"
- ❌ "Refactored webpack config and optimized chunks"

**Use imperative mood** (command form)
- ✅ "Add dark mode support"
- ❌ "Added dark mode support" or "Adds dark mode support"

**Be specific**
- ✅ "Fixed SQL injection in search endpoint"
- ❌ "Fixed security issue"

**Link to issues/PRs**
- ✅ "Added user profile page ([#123](link))"
- Gives credit and provides context

**Group related changes**
- Instead of 10 separate "Fixed typo in..." entries, group them:
- ✅ "Fixed typos in user documentation"

### Don't ❌

**Don't list every commit**
- Changelogs are curated, not exhaustive
- Combine related commits into single entries

**Don't use git commit messages directly**
- "WIP", "fix typo", "oops" are not helpful

**Don't include internal refactoring without user impact**
- Users don't care that you renamed variables
- Exception: If refactoring improves performance or fixes bugs

**Don't use passive voice**
- ❌ "Bug was fixed"
- ✅ "Fixed bug"

**Don't be vague**
- ❌ "Various improvements"
- ✅ "Improved search performance by indexing user names"

**Don't forget to credit contributors**
- Include usernames or links when appropriate

## Generating Changelogs

### Manual Curation

1. **Review all commits** since last release
   ```bash
   git log v1.1.0..HEAD --oneline
   ```

2. **Group commits** by category (Added, Fixed, etc.)

3. **Rewrite commit messages** for clarity

4. **Remove noise** (internal refactoring, minor tweaks)

5. **Add context** where needed

### Automated Generation

Tools that can generate changelogs from commit messages:

**standard-version**
```bash
npm install -g standard-version
standard-version
```

**conventional-changelog**
```bash
npm install -g conventional-changelog-cli
conventional-changelog -p angular -i CHANGELOG.md -s
```

**auto-changelog**
```bash
npm install -g auto-changelog
auto-changelog
```

### Hybrid Approach (Recommended)

1. Use automated tools to **generate draft**
2. **Review and edit** for clarity
3. **Add context** that tools can't infer
4. **Reorder** for logical flow
5. **Remove** irrelevant entries

## Changelog for Different Audiences

### Internal/Technical Changelog
- More detailed
- Include breaking changes with migration paths
- Link to technical discussions
- List deprecated APIs

### User-Facing Release Notes
- Focus on benefits, not technical details
- Use screenshots or GIFs for UI changes
- Highlight top 3-5 changes
- Simplify technical language

### Example Transformation

**Technical Changelog**:
```
### Changed
- Migrated authentication from JWT to OAuth2
- Updated API response format from XML to JSON
```

**User-Facing Release Notes**:
```
### Improved
- You can now log in with your Google or GitHub account!
- Faster API responses with improved data format
```

## Special Changelog Scenarios

### First Release (1.0.0)

```markdown
## [1.0.0] - 2024-01-15

### Added
- Initial release
- [List key features that ship in v1]
```

### Pre-Release Versions

```markdown
## [1.0.0-beta.1] - 2024-01-10

### Added
- Beta release for testing
- All planned v1.0.0 features included

### Known Issues
- Performance optimization in progress
- UI refinements needed
```

### Hotfix Releases

```markdown
## [1.2.1] - 2024-01-16

### Fixed
- **CRITICAL**: Fixed authentication bypass vulnerability (CVE-2024-XXXXX)

### Security
- Users should upgrade immediately
```

### Major Version with Breaking Changes

```markdown
## [2.0.0] - 2024-02-01

### Breaking Changes ⚠️
- Removed support for Node.js <16
- Changed API endpoint format from `/api/v1/users` to `/v2/users`
- Replaced `getUserData()` with `fetchUser()` (see migration guide)

### Migration Guide
See [MIGRATION.md](MIGRATION.md) for detailed upgrade instructions.

### Added
- New webhook system for real-time updates
- GraphQL API alongside REST

### Removed
- Deprecated XML format support (use JSON)
```

## Changelog Best Practices

1. **Update with every release**, not retroactively
2. **Keep a `[Unreleased]` section** at the top for tracking ongoing work
3. **Be consistent** with formatting and categories
4. **Date everything** using ISO 8601 format
5. **Make it skimmable** with clear headers and formatting
6. **Tell a story** of how the project evolves
7. **Celebrate contributors** by crediting them
8. **Link generously** to issues, PRs, and documentation
9. **Write for your least technical user**
10. **Keep it in the repository** (usually `CHANGELOG.md` at root)

## Anti-Patterns

❌ **Dumping all git commit messages** into changelog
❌ **Forgetting to update** changelog before release
❌ **Vague entries** like "Bug fixes and improvements"
❌ **Only listing features**, ignoring fixes and breaking changes
❌ **No dates or version numbers**
❌ **Changelog only in release notes**, not in repository
❌ **Too technical** for end users
❌ **Missing security fixes**

## Tools and Resources

**Changelog Validators**:
- [keepachangelog.com](https://keepachangelog.com/)

**Commit Message Linters**:
- commitlint: Enforce conventional commit format
- husky: Git hooks for commit validation

**Changelog Generators**:
- standard-version
- semantic-release
- conventional-changelog
- auto-changelog

**Examples of Great Changelogs**:
- React: https://github.com/facebook/react/blob/main/CHANGELOG.md
- Angular: https://github.com/angular/angular/blob/main/CHANGELOG.md
- Node.js: https://github.com/nodejs/node/blob/main/CHANGELOG.md
