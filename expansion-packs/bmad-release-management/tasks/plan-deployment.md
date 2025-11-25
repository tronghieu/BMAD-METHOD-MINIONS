# Task: Plan Deployment

**Release Management Phase**: Deployment Planning
**Duration**: 30-60 minutes
**Agent**: Deployment Coordinator
**Difficulty**: Medium-High

## Purpose

To create a detailed, step-by-step deployment runbook that ensures a safe, predictable, and repeatable release to production.

## Prerequisites

- The release has passed all quality gates and received a "Go" decision.
- The release scope, including any database changes, is finalized.
- A target deployment window has been scheduled.

## High-Level Process

As the Deployment Coordinator, your goal is to create the official deployment runbook. Use the `data/deployment-planning-guide.md` for detailed methodology on each phase.

### 1. Select Deployment Strategy
- [ ] Based on the release's risk profile, select the appropriate deployment pattern (e.g., Blue-Green, Canary, Rolling).
- [ ] Document the chosen strategy and the rationale.
- [ ] Refer to `data/deployment-patterns.md` for detailed information on each pattern.

### 2. Plan Database Migrations
- [ ] Detail the sequence of all database migration scripts.
- [ ] For any breaking changes, specify the use of the Expand-Contract pattern.
- [ ] Document a clear, tested rollback plan for the database changes.

### 3. Define Deployment Runbook
- [ ] Break the deployment into a chronological sequence of phases (Pre-Deployment, Migration, App Deployment, Smoke Testing, Monitoring).
- [ ] For each step, specify the exact command, the expected outcome, and a verification check.
- [ ] Use `checklists/deployment-checklist.md` as a guide for required steps.

### 4. Create Rollback Procedure
- [ ] Define the specific, measurable triggers that will initiate a rollback (e.g., error rate thresholds).
- [ ] Document the precise, step-by-step commands to revert the deployment.
- [ ] Assign a primary and backup owner for the rollback decision.
- [ ] Refer to `checklists/rollback-checklist.md` for emergency procedures.

### 5. Finalize and Document
- [ ] Assign roles and responsibilities for the deployment team.
- [ ] Review the complete runbook with the team.
- [ ] **Action**: Use the `deployment-plan.yaml` template to generate the final `deployment-plan.md` document.

## Expected Outputs

- A comprehensive **`deployment-plan.md`** (runbook) containing:
  - The chosen deployment strategy and rationale.
  - A phase-by-phase execution plan with specific commands and verification steps.
  - A detailed and tested rollback procedure with clear triggers.
  - A list of team roles and responsibilities.

## Related Resources
- **Methodology Guide**: `data/deployment-planning-guide.md`
- **Pattern Library**: `data/deployment-patterns.md`
- **Execution Checklists**: `checklists/deployment-checklist.md`, `checklists/rollback-checklist.md`
- **Output Template**: `templates/deployment-plan.yaml`
