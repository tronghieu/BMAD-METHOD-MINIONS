# Versioning Strategies Guide

## Overview

Version numbers are not just labels—they communicate expectations about compatibility, risk, and upgrade effort to your users. Choosing the right versioning strategy and applying it consistently builds trust with your user base.

## Semantic Versioning (SemVer)

### Format: MAJOR.MINOR.PATCH (e.g., 2.4.1)

Semantic Versioning is the most widely adopted versioning scheme in software development. It provides clear signals about the nature of changes.

### Version Number Meaning

**MAJOR** (leftmost number)
- Increment when you make **breaking changes**
- Users must modify their code to upgrade
- Example: API endpoint removed, parameter renamed, behavior changed

**MINOR** (middle number)
- Increment when you add **new features** (backward compatible)
- Users can upgrade without code changes
- Existing functionality continues to work
- Example: New API endpoint added, new optional parameter

**PATCH** (rightmost number)
- Increment for **bug fixes** (backward compatible)
- No new features, just fixes
- Users should always upgrade patches
- Example: Fixed crash, corrected calculation, performance improvement

### SemVer Examples

```
1.0.0 → 1.0.1  (patch: bug fix)
1.0.1 → 1.1.0  (minor: new feature)
1.1.0 → 2.0.0  (major: breaking change)
2.0.0 → 2.0.1  (patch: bug fix)
```

### When to Use SemVer

✅ **Best for**:
- Libraries and APIs
- Open source projects
- Developer tools
- Any software with programmatic interfaces

✅ **Why**:
- Clear expectations about compatibility
- Widely understood by developers
- Supported by package managers (npm, pip, cargo, etc.)
- Enables dependency management (e.g., "^1.2.0" = "1.x.x but not 2.x.x")

### SemVer Rules

1. **Start at 0.1.0** for initial development
2. **Release 1.0.0** when your API is stable and production-ready
3. **Pre-release versions** use hyphen: `1.0.0-alpha`, `1.0.0-beta.1`, `1.0.0-rc.1`
4. **Build metadata** uses plus: `1.0.0+20240115`
5. **Never reuse** a version number (even if you delete it)

### What Counts as a Breaking Change?

**Definitely Breaking**:
- Removing endpoints, functions, or classes
- Renaming parameters or fields
- Changing parameter types
- Changing return value structure
- Changing default behavior that users rely on
- Removing or changing error codes

**Possibly Breaking** (use judgment):
- Deprecating (but not removing) functionality
- Adding required parameters
- Tightening validation
- Changing performance characteristics significantly

**Not Breaking**:
- Adding optional parameters with defaults
- Adding new endpoints or functions
- Improving error messages
- Bug fixes (unless users were relying on the bug!)

## Calendar Versioning (CalVer)

### Format: YYYY.MM.DD or YY.MM.MICRO (e.g., 2024.01.15 or 24.1.3)

Calendar Versioning uses dates as version numbers, signaling when software was released rather than what changed.

### Common CalVer Formats

**YYYY.MM.DD** (e.g., 2024.01.15)
- Full year, month, day
- Best for: Frequent releases, time-based distributions

**YYYY.MM.MICRO** (e.g., 2024.01.3)
- Full year, month, incrementing number
- Best for: Monthly release cycles with multiple releases per month

**YY.0M.MICRO** (e.g., 24.01.3)
- Short year, zero-padded month, incrementing number
- Best for: Shorter version strings

**YYYY.0W.MICRO** (e.g., 2024.03.2)
- Year, week number, incrementing number
- Best for: Weekly release cadences

### When to Use CalVer

✅ **Best for**:
- Consumer applications (Ubuntu, Windows)
- Rapidly evolving products
- Time-based releases (monthly, quarterly)
- Products with marketing-driven versioning

✅ **Why**:
- Immediately shows age of software
- Easier for non-technical users to understand
- Works well with continuous delivery
- Signals regular release cadence

### CalVer Examples

```
Ubuntu: 22.04 (released April 2022), 22.10 (October 2022)
Windows: 20H1 (2020, first half), 21H2 (2021, second half)
```

### CalVer Considerations

**Advantages**:
- Shows currency of software at a glance
- No ambiguity about release order
- Marketing-friendly ("2024 version")

**Disadvantages**:
- Doesn't signal breaking changes
- Can't use dependency ranges like SemVer
- May imply software is outdated if not updated monthly

## Marketing Versioning

### Format: Any meaningful number (e.g., Windows 11, iPhone 15, Photoshop 2024)

Marketing versions prioritize user communication over technical meaning.

### When to Use Marketing Versions

✅ **Best for**:
- Consumer products
- Products with major yearly releases
- Brand positioning

### Examples

- **Windows**: 7 → 8 → 10 → 11
- **macOS**: Big Sur → Monterey → Ventura → Sonoma
- **Adobe**: CC 2020 → CC 2021 → CC 2023

### Dual Versioning

Many products use both marketing and technical versions:
- **User-facing**: "Photoshop 2024"
- **Technical**: "25.0.1"

## Choosing Your Strategy

### Decision Tree

```
Are you building a library or API?
├─ YES → Use Semantic Versioning (SemVer)
└─ NO → Is your product consumer-facing?
    ├─ YES → Use Calendar Versioning (CalVer) or Marketing Versioning
    └─ NO → Do you have time-based releases?
        ├─ YES → Use Calendar Versioning (CalVer)
        └─ NO → Use Semantic Versioning (SemVer)
```

### Comparison Table

| Factor | SemVer | CalVer | Marketing |
|--------|--------|--------|-----------|
| **Signals compatibility** | ✅ Yes | ❌ No | ❌ No |
| **Signals age** | ❌ No | ✅ Yes | Sometimes |
| **Developer-friendly** | ✅ Yes | Partial | ❌ No |
| **User-friendly** | Partial | ✅ Yes | ✅ Yes |
| **Dependency management** | ✅ Yes | ❌ No | ❌ No |
| **Time-based releases** | ❌ No | ✅ Yes | ✅ Yes |

## Pre-Release Versions

### Alpha (α)
- **Format**: `1.0.0-alpha` or `1.0.0-alpha.1`
- **Meaning**: Very early, internal testing
- **Stability**: Unstable, features incomplete
- **Audience**: Internal team only

### Beta (β)
- **Format**: `1.0.0-beta` or `1.0.0-beta.2`
- **Meaning**: Feature complete, needs testing
- **Stability**: Mostly stable, bugs expected
- **Audience**: Early adopters, testers

### Release Candidate (RC)
- **Format**: `1.0.0-rc.1`
- **Meaning**: Final testing before release
- **Stability**: Should be stable, only critical bugs fixed
- **Audience**: Broader testing audience

### Pre-Release Progression

```
1.0.0-alpha.1 → 1.0.0-alpha.2 → 1.0.0-beta.1 → 1.0.0-beta.2 → 1.0.0-rc.1 → 1.0.0
```

## Version Bumping Rules

### For SemVer

**Breaking Change Found?**
- YES → Bump MAJOR, reset MINOR and PATCH to 0
  - `1.4.7 → 2.0.0`

**New Feature Added?** (no breaking changes)
- YES → Bump MINOR, reset PATCH to 0
  - `1.4.7 → 1.5.0`

**Bug Fixes Only?**
- YES → Bump PATCH
  - `1.4.7 → 1.4.8`

### Special Cases

**Multiple Changes in One Release**
- If you have both breaking changes AND new features → Bump MAJOR
- If you have both new features AND bug fixes → Bump MINOR
- Always apply the highest level of change

**Hotfix from Old Version**
- If fixing 2.3.1 while 2.5.0 exists → Release 2.3.2
- Maintain old versions when users can't upgrade immediately

## Version Control Integration

### Git Tags

Always tag releases in git:
```bash
git tag -a v1.2.3 -m "Release version 1.2.3"
git push origin v1.2.3
```

### Branch Strategies

**GitFlow**:
- `main` or `master` → production releases only
- `develop` → integration branch
- `release/1.2.0` → release preparation branches
- `hotfix/1.2.1` → urgent production fixes

**Trunk-Based**:
- `main` → always releasable
- Feature flags for incomplete features
- Rapid releases

## Deprecation Policy

When planning breaking changes, follow a graceful deprecation process:

### Standard Deprecation Timeline

1. **Announce deprecation** (Release N)
   - Mark feature as deprecated in docs
   - Add deprecation warnings in code
   - Provide migration path

2. **Maintain deprecated feature** (Release N+1)
   - Keep functionality working
   - Remind users in release notes

3. **Remove deprecated feature** (Release N+2, MAJOR version)
   - Remove functionality
   - Update documentation

### Example

```
v1.4.0: Announce deprecation of oldMethod(), introduce newMethod()
v1.5.0: oldMethod() still works, shows deprecation warning
v2.0.0: oldMethod() removed, only newMethod() available
```

## Version Number Edge Cases

### When to Skip Versions

**Never skip versions**. Even if it feels "cleaner" to jump from 1.9 to 2.0, don't skip intermediate numbers. It creates confusion in the version history.

### When to Reset to 1.0.0

- Complete rewrite/redesign
- New product name
- Breaking changes so significant that it's essentially a new product

### Zero Major Version (0.x.x)

- `0.x.x` signals "in development, not production-ready"
- Breaking changes can happen in MINOR versions during 0.x.x
- Once stable, release 1.0.0

## Tools and Automation

### Version Bumping Tools

- **npm version**: Built into npm (`npm version patch|minor|major`)
- **standard-version**: Automated versioning and changelog generation
- **semantic-release**: Fully automated versioning from commits

### Commit Message Conventions

Use Conventional Commits to automate version bumps:

```
fix: Fixed login bug          → PATCH bump
feat: Added dark mode         → MINOR bump
feat!: Changed API format     → MAJOR bump
```

## Best Practices

1. **Be Consistent**: Pick a strategy and stick to it
2. **Communicate Changes**: Always explain what changed in release notes
3. **Automate When Possible**: Use tools to reduce manual errors
4. **Document Your Strategy**: Tell users how you version
5. **Respect Semantic Meaning**: Don't lie with version numbers
6. **Plan Breaking Changes**: Group them together when possible
7. **Maintain Old Versions**: Support security patches for older versions when feasible

## Anti-Patterns to Avoid

❌ **Random version bumps** (1.0 → 1.5 with no clear reason)
❌ **Marketing pressure** (skipping to v10.0 to look mature)
❌ **Breaking changes in patches** (breaks user trust)
❌ **Reusing deleted version numbers**
❌ **Never reaching 1.0.0** (everything is 0.x.x forever)
