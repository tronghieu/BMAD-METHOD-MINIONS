# Scope Analysis Checklist

Use this checklist to systematically review and identify all work items to be considered for inclusion in the upcoming release. This ensures a comprehensive understanding of the release scope and minimizes missed items.

## 1. Review Git History

- [ ] Review all commits between the last release tag (e.g., `v{{last_release_version}}`) and the current `HEAD` of the main branch.
  - `git log v{{last_release_version}}..HEAD --oneline`
- [ ] Identify significant changes by commit message type (e.g., `feat:`, `fix:`, `BREAKING CHANGE:`).
- [ ] List potential work items based on commit messages.

## 2. Review Issue Tracker

- [ ] Check all issues/tickets marked as "Done" or "Closed" since the last release.
  - *Example:* Filter by `status = Done AND resolved >= {{last_release_date}}`
- [ ] Review relevant project boards or milestones for completed items.
- [ ] Verify that identified issues/PRs are linked to corresponding commits (if applicable).

## 3. Review Completed Pull Requests/Merge Requests

- [ ] List all Pull Requests (GitHub) or Merge Requests (GitLab) that have been merged into the main branch since the last release.
- [ ] Ensure that each merged PR corresponds to a known issue or planned feature.

## 4. Identify Feature Flags

- [ ] Review the status of all feature flags in the codebase.
- [ ] Identify any new features developed under flags that are ready for enablement.
- [ ] Confirm the default state of these flags for the release (on/off).

## 5. Consult with Team Leads/Product Owners

- [ ] Discuss with engineering leads about any significant un-ticketed work (e.g., major refactoring, performance improvements, technical debt paid down).
- [ ] Confirm with the Product Owner the list of user-facing features intended for this release.
- [ ] Inquire about any known issues or last-minute changes not yet reflected in git or the issue tracker.

## 6. Work Item Categorization

For each identified work item, assign a category:

- [ ] **Feature (New/Added)**: New functionality, user-facing capabilities, new APIs.
- [ ] **Enhancement (Changed)**: Improvements to existing features, modified behavior (backward compatible).
- [ ] **Bug Fix (Fixed)**: Resolved defects, crashes, incorrect calculations.
- [ ] **Breaking Change (⚠️)**: Incompatible API changes, removed features, significant behavioral shifts requiring user migration.
- [ ] **Security Fix (🔒)**: Vulnerability patches, security improvements.
- [ ] **Performance Improvement**: Speed optimizations, resource reduction.
- [ ] **Documentation Update**: Significant updates to user guides, API docs.
- [ ] **Internal/Infrastructure**: CI/CD improvements, build system changes (typically not user-facing).

## 7. Assess Work Item Readiness

For each work item proposed for inclusion:

- [ ] **Code Merged**: All code is in the main branch.
- [ ] **Tests Passing**: Unit, integration, and E2E tests are green.
- [ ] **Code Reviewed**: All relevant code has been reviewed and approved.
- [ ] **Documentation Updated**: User and technical documentation reflects changes.
- [ ] **No Known Critical Issues**: No critical bugs or regressions are pending.
- [ ] **Dependencies Met**: All internal and external dependencies are resolved.

## 8. Final Scope Recommendation

- [ ] Based on the assessment, recommend items for:
  - **INCLUDE**: Ready to ship, aligns with release goals.
  - **DEFER**: Not ready, low priority, or too risky for this release.
  - **CONDITIONAL**: Needs further discussion/validation before decision.
- [ ] Document the rationale for any deferrals.
- [ ] Document any identified risks associated with included items.
- [ ] Get initial alignment from Product Owner and Engineering Lead on recommended scope.

## Sign-Off

- [ ] **Scope Analyzer**: _________________ Date: _______
- [ ] **Product Owner**: _________________ Date: _______
- [ ] **Engineering Lead**: _________________ Date: _______
