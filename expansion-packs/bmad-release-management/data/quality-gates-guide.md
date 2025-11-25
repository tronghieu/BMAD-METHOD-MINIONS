# Quality Gates Guide

This guide provides the methodology behind running comprehensive quality gates. It is intended to be used by the `Quality Gatekeeper` agent when executing the `run-quality-gates` task.

## Purpose
Quality gates are objective, automated, and manual checkpoints that a release must pass before it can be deployed. The purpose of this process is to protect production from broken, insecure, or performant-degrading releases and to make the go/no-go decision an evidence-based one, not an emotional one.

## Core Principles
- **Automation First:** Automate as many gates as possible to ensure consistency and speed.
- **Evidence-Based:** Decisions must be backed by data from test results, scan reports, and performance metrics.
- **Risk Assessment:** Not all failures are equal. The goal is to understand and mitigate risk, not to achieve a theoretical "perfection."
- **Zero Tolerance for Critical Issues:** Critical test failures and security vulnerabilities must block a release.

## Quality Gate Phases

### Phase 1: Test Coverage & Execution
This gate validates that the software is functionally correct and that changes have not introduced regressions.
- **Action:** Execute the full test suite (unit, integration, end-to-end).
- **Verify:** All tests must pass. No flaky tests should be present.
- **Action:** Generate a code coverage report.
- **Verify:** Coverage must meet the team-defined threshold (e.g., >80%). Critical code paths must have near 100% coverage.

### Phase 2: Security Scanning
This gate ensures the release does not introduce new security vulnerabilities.
- **Action:** Run SAST (Static), DAST (Dynamic), and dependency scanning tools.
- **Verify:** There must be a zero-tolerance policy for new Critical or High-severity vulnerabilities. Medium and Low findings should be reviewed, assessed, and have a remediation plan.

### Phase 3: Performance Validation
This gate confirms that the new release performs as well as, or better than, the previous version.
- **Action:** Run automated load tests against a staging environment.
- **Verify:** Key metrics (p95/p99 response time, throughput, error rate under load) must not have regressed beyond a set threshold (e.g., >10% degradation).

### Phase 4: Functional Validation in Staging
This gate is a final check of the complete release artifact in a production-like environment.
- **Action:** Deploy the release to the staging environment.
- **Action:** Execute a series of automated or manual smoke tests covering critical user journeys (e.g., login, core feature usage, checkout).
- **Verify:** All smoke tests must pass.

### Phase 5: Documentation & Release Preparation
This gate ensures the release is ready for users and support teams.
- **Action:** Review all user-facing and technical documentation.
- **Verify:** Release notes must be complete, migration guides (if any) must be accurate, and support documentation must be updated.

## Go/No-Go Recommendation
After assessing all gates, the `Quality Gatekeeper` synthesizes the results into a final recommendation.
- **GO:** All critical gates passed. The release is high quality and low risk.
- **NO-GO:** One or more critical gates failed. The release is not safe to ship. It must be blocked until issues are resolved.
- **CONDITIONAL GO:** All critical gates passed, but some important gates have acceptable failures (e.g., a known low-impact bug, a documented performance trade-off). The release can proceed if stakeholders formally accept the documented risks.

The final output is the `quality-assessment-plan.md`, which serves as the official record of the quality assessment and the final sign-off for the release to proceed to deployment.
