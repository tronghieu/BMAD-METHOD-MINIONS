# Rollback Guide

This guide provides the methodology for executing an emergency rollback. It is intended for use by the `Deployment Coordinator` when the `rollback-release` task is initiated.

## Purpose
A rollback is an emergency procedure to rapidly revert a production environment to its last known good state. It is a critical safety mechanism, not a failure. The primary goal is to restore service and minimize user impact as quickly as possible.

## Core Principles
- **Speed is Critical:** The priority is to stop the bleeding. Restore service first, then diagnose the cause.
- **Act Decisively:** When rollback criteria are met, do not hesitate. A bad deployment rarely gets better on its own.
- **Communicate Clearly:** Declare an incident and keep stakeholders informed with concise, regular updates.
- **Follow the Plan:** Execute the pre-planned rollback procedure from the deployment runbook. Do not improvise under pressure.

## Rollback Execution Phases

### Phase 1: Decision and Communication (T+0 to T+5 minutes)
This is the immediate response once a critical issue is detected.
- **Assess Severity:** Quickly determine if the issue meets the pre-defined rollback triggers (e.g., error rate > 5%, core functionality broken).
- **Declare an Incident:** This is a formal step. Create a dedicated communication channel, assign an incident commander, and announce that a rollback is being initiated.
- **Assemble the Team:** Page the deployment team and on-call engineers.
- **Notify Stakeholders:** A simple "Initiating rollback due to [issue]. ETA [time]." is sufficient to start.

### Phase 2: Execute Rollback (T+5 to T+30 minutes)
This phase involves executing the technical steps to revert the system. The exact steps depend on the deployment pattern used and should be documented in the `deployment-plan.md` for the release. The `rollback-checklist.md` provides the generic execution steps.
- **Execute Application Rollback:** Revert the application code. This could be as simple as switching a load balancer (Blue-Green) or as involved as re-deploying the previous version (Rolling/Recreate).
- **Execute Database Rollback (If Absolutely Necessary):** This is the most dangerous step.
  - **Best Case:** The old application code is compatible with the new database schema (if you used the Expand-Contract pattern). No database rollback is needed.
  - **Acceptable Case:** Run "down" migration scripts to reverse the schema changes. This carries a risk of data loss.
  - **Last Resort:** Restore the database from the pre-deployment backup. This *will* cause data loss for any transactions that occurred after the backup was taken. This requires leadership approval.

### Phase 3: Verification (T+15 to T+45 minutes)
After executing the rollback, you must verify that the service is restored.
- **Confirm Version:** Ensure the old, stable version of the application is running.
- **Check Health:** Verify that health checks are passing and error rates are returning to baseline levels.
- **Smoke Test:** Perform a quick manual test of the most critical user functionality (login, etc.).

### Phase 4: Communication and Post-Mortem Prep
Once the service is stable, close out the incident.
- **Communicate Resolution:** Update the status page and notify all stakeholders that the issue is resolved. Be transparent that a rollback was performed.
- **Document the Incident:** While the details are fresh, create an incident report detailing the timeline, impact, and resolution.
- **Preliminary RCA:** Begin a preliminary root cause analysis.
- **Schedule Post-Mortem:** Book a blameless post-mortem meeting within 24-48 hours to learn from the incident.

A successful rollback is one that is fast, safe, and effective. Every rollback is a valuable learning opportunity to improve the entire release process.
