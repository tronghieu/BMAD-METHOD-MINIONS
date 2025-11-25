# Scope Analysis Guide

This guide provides a detailed methodology for analyzing the scope of an upcoming release. It is intended to be used by the `Scope Analyzer` agent when executing the `analyze-scope` task.

## Purpose
The goal of scope analysis is to systematically review all completed work since the last release to determine what should be included in the upcoming release. This process ensures nothing important is missed and helps identify items that are not ready and should be deferred. A well-defined scope is the foundation of a predictable release.

## Phase 1: Gather Work Items
The first step is to create a comprehensive inventory of all potential items for the release.

#### 1.1 Review Git History
Examine all commits since the last release tag to find code changes.
- **Action:** Use `git log v{{last_version}}..HEAD` to list commits.
- **Look for:** Commits prefixed with `feat`, `fix`, `BREAKING CHANGE`, `perf`, and `security`. These indicate significant changes.

#### 1.2 Review Issue Tracker
Check project management tools (Jira, GitHub Issues, etc.) for completed work.
- **Action:** Filter for items moved to a "Done" or "Resolved" state since the last release date.
- **Look for:** Issues, stories, or tasks associated with the current release milestone.

#### 1.3 Gather Team Input
Automated tools don't catch everything.
- **Action:** Consult with development team leads.
- **Ask:** "Is there any significant work completed that isn't tracked in an issue? Any major refactoring or technical debt work we should be aware of?"

## Phase 2: Categorize Changes
Organize the raw list of work items into standard categories to bring structure to the release. For detailed definitions, the agent should rely on its common knowledge of "Keep a Changelog" conventions.
- **Breaking Changes ⚠️**
- **Features (Added)**
- **Enhancements (Changed)**
- **Bug Fixes (Fixed)**
- **Security Fixes** 🔒
- **Performance Improvements**
- **Documentation**
- **Infrastructure/Internal**

## Phase 3: Assess Readiness
For each item, determine if it meets the "Definition of Done."
- **Is it complete?** Code merged, tests passing, reviewed, and documented.
- **Is it tested?** Sufficient unit, integration, and manual testing completed. QA has approved.
- **Is it documented?** User-facing changes have corresponding documentation updates. Breaking changes have a migration guide.
- **Does it have known issues?** No critical or high-severity bugs.

Based on this assessment, assign a status: `INCLUDE`, `DEFER`, `CONDITIONAL`, or `INVESTIGATE`.

## Phase 4: Identify Dependencies
Map the relationships between work items to avoid shipping a feature that depends on another deferred item.
- **Code Dependencies:** "Feature A requires Feature B's API."
- **Team Dependencies:** "Backend change requires a mobile app update."
- **Sequential Dependencies:** "Database migration must run before the application is deployed."

## Phase 5: Make Inclusion Recommendations
Based on the analysis, create a final recommendation for the release scope.

#### 5.1 Apply Inclusion Criteria
- **Must Include:** Security fixes, critical bug fixes, committed features, and dependencies of other included items.
- **Should Include:** Completed features aligned with release goals, important bug fixes.
- **Consider Deferring:** Incomplete or high-risk changes, items with known bugs.
- **Must Defer:** Code not merged, failing tests, missing documentation for user-facing changes.

#### 5.2 Assess Scope Balance
- **Is the scope too large?** A high number of items or multiple high-risk changes increases the chance of failure. **Recommendation:** Split the release or defer lower-priority items.
- **Is the scope too small?** If the release contains only a few minor fixes, it may not be worth the overhead. **Recommendation:** Consider bundling with the next release unless the fixes are critical.

#### 5.3 Document Recommendations
Create a clear, final list of what is IN and what is OUT.
- **Inclusion List:** A list of all features and fixes that will be in the release.
- **Deferral List:** A list of items that will be moved to a future release, with a brief reason for each deferral.
- **Items for Discussion:** Any items where the inclusion decision requires further input from product or engineering leadership.

## Phase 6: Review and Finalize
Share the documented scope with the Release Manager, Product Owner, and Engineering Lead to get formal sign-off. This final, agreed-upon scope is then added to the main release plan document.
