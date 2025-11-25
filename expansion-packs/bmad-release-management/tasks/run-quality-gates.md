# Task: Run Quality Gates

**Release Management Phase**: Quality Validation
**Duration**: 30-90 minutes
**Agent**: Quality Gatekeeper
**Difficulty**: Medium-High

## Purpose

To systematically validate that a release candidate meets all defined quality standards before deployment, culminating in an evidence-based "Go/No-Go" decision.

## Prerequisites

- The release scope is finalized and all code has been merged.
- A release candidate is built and deployed to a production-like staging environment.
- Access to all testing, security, and performance tooling is available.
- The `pre-release-checklist.md` is available.

## High-Level Process

As the Quality Gatekeeper, your responsibility is to act as the guardian of production stability. Use the `checklists/pre-release-checklist.md` as your execution guide and refer to `data/quality-gates-guide.md` for the detailed methodology behind each gate.

### 1. Validate Test Suite
- [ ] Confirm that all automated tests (unit, integration, E2E) are passing in the CI/CD pipeline.
- [ ] Verify that code coverage meets or exceeds the defined team threshold (e.g., 80%).

### 2. Validate Security Gates
- [ ] Execute all security scans (SAST, DAST, Dependency).
- [ ] Confirm there are zero new Critical or High-severity vulnerabilities. Triage and document any lower-severity findings.

### 3. Validate Performance Gates
- [ ] Run performance and load tests against the staging environment.
- [ ] Confirm that performance metrics (response time, throughput) have not regressed beyond the acceptable threshold (e.g., 10%).

### 4. Validate Functional Gates
- [ ] Perform smoke tests on the staging environment to verify critical user paths are working as expected.
- [ ] Ensure all documentation (user guides, release notes, migration paths) is complete and accurate.

### 5. Synthesize and Recommend
- [ ] Consolidate all results from the quality gates.
- [ ] Make a final, evidence-based recommendation: **GO**, **NO-GO**, or **CONDITIONAL GO**.
- [ ] If the recommendation is not a clear "GO", document all risks, failing gates, and required conditions for proceeding.

## Expected Outputs

- A completed **`quality-assessment-plan.md`** document, generated from the `quality-assessment-plan.yaml` template. This report will contain:
  - The status of all quality gates.
  - A summary of any identified risks.
  - The final "Go/No-Go" recommendation.
  - A section for stakeholder sign-offs.

## Related Resources
- **Execution Checklist**: `checklists/pre-release-checklist.md`
- **Methodology Guide**: `data/quality-gates-guide.md`
- **Output Template**: `templates/quality-assessment-plan.yaml`
- **Knowledge Base**: `data/release-management-kb.md`
