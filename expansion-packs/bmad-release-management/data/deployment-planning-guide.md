# Deployment Planning Guide

This guide provides the methodology for creating a detailed deployment plan (runbook). It is intended to be used by the `Deployment Coordinator` agent when executing the `plan-deployment` task.

## Purpose
A deployment plan, or runbook, is a detailed, step-by-step set of instructions for deploying a release to production. Its purpose is to ensure the deployment is predictable, repeatable, and safe. A good runbook minimizes human error and reduces stress during the deployment window.

## Core Principles
- **Clarity and Precision:** Every step should be unambiguous. Include exact commands to be run.
- **Verification at Every Step:** After each significant action, include a step to verify it was successful.
- **Plan for Failure:** A robust rollback plan is the most critical part of any deployment plan.
- **Team Alignment:** Everyone on the deployment team should review and understand the plan before execution.

## Deployment Planning Phases

### Phase 1: Select Deployment Strategy
The first and most important decision is choosing *how* to deploy. This choice depends on the release's risk, the application's architecture, and business requirements. For detailed explanations of each pattern, refer to `data/deployment-patterns.md`.

- **Action:** Assess the release risk (breaking changes, user impact, rollback complexity).
- **Action:** Select the most appropriate deployment pattern:
  - **Blue-Green:** Best for high-risk releases needing instant rollback.
  - **Canary:** Best for gradually testing new features with a subset of users.
  - **Rolling:** A good default for standard, backward-compatible releases.
  - **Feature Flags:** Best for decoupling code deployment from feature release.
  - **Recreate:** Only for non-critical systems where downtime is acceptable.
- **Action:** Document the chosen strategy and the rationale behind it.

### Phase 2: Plan Database Migrations
Database changes are often the riskiest part of a deployment.
- **Action:** List all required database migration scripts in the order they must be executed.
- **Action:** For breaking schema changes, plan to use the **Expand-Contract pattern** to ensure zero-downtime and rollback safety. This is detailed in `data/deployment-patterns.md`.
- **Action:** Create and test a specific rollback plan for the database migrations. This may involve "down" migration scripts or restoring from a backup (a last resort).

### Phase 3: Define Deployment Phases (Create the Runbook)
Break the entire deployment process into a clear, chronological sequence of phases and steps.

- **Phase 1: Pre-Deployment:** All tasks to be completed *before* the deployment begins (e.g., create backups, health check production, notify team).
- **Phase 2: Database Migration:** Steps to apply database changes.
- **Phase 3: Application Deployment:** Steps to roll out the new application code, following the chosen strategy (Blue-Green, Rolling, etc.).
- **Phase 4: Smoke Testing:** A critical set of post-deployment tests to verify core functionality is working.
- **Phase 5: Monitoring:** A brief period of intensive monitoring to confirm the release is stable before declaring success.

For each step, include the exact command to be run, the expected outcome, and a verification command.

### Phase 4: Create Rollback Procedures
Every deployment plan must have a clear, tested rollback plan.
- **Action:** Define the specific triggers for a rollback (e.g., "error rate > 5%" or "core checkout feature fails smoke test").
- **Action:** Document the step-by-step procedure to revert to the previous stable version. This procedure will be specific to the chosen deployment pattern.
- **Action:** Assign a clear owner for the rollback decision (e.g., the Release Manager or on-call lead).

### Phase 5: Assign Roles and Finalize
- **Action:** Assign clear roles for the deployment window: Deployment Lead, Technical Executor, Monitoring Observer, etc.
- **Action:** Review the complete runbook with the entire deployment team to ensure everyone understands their role and the plan.
- **Action:** Generate the final `deployment-plan.md` document from the `deployment-plan.yaml` template.

The resulting runbook should be so clear that a person unfamiliar with the deployment could execute it successfully.
