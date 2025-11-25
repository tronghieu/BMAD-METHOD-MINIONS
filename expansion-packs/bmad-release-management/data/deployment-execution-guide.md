# Deployment Execution Guide

This guide provides a detailed methodology for executing a planned deployment. It is intended to be used by the `Deployment Coordinator` and the deployment team during the execution of the `execute-deployment` task.

## Purpose
The goal of this phase is to safely and predictably deploy the new release to production by following the pre-approved deployment plan (runbook). The focus is on careful execution, continuous monitoring, and clear communication.

## Core Principles
- **Follow the Plan:** Do not deviate from the approved deployment runbook unless absolutely necessary.
- **Communicate Constantly:** Keep all stakeholders informed of progress, especially if issues arise.
- **Verify, Then Proceed:** After every major step, verify its success before moving to the next.
- **When in Doubt, Rollback:** It is always safer to roll back a questionable deployment than to push forward and hope for the best.

## Deployment Execution Phases

### Phase 1: Pre-Deployment (T-60 to T-0 minutes)
This is the final preparation window before the deployment begins.
- **Assemble Team:** Get the assigned deployment team (Lead, Executor, Monitor, etc.) on a dedicated communication channel.
- **Final Health Check:** Verify that the production environment is stable and healthy *before* you introduce any changes. A deployment should never start during an ongoing incident.
- **Create Backups:** Take final backups of databases and critical configurations. Verify that the backups are valid and restorable.
- **Notify Stakeholders:** Announce that the deployment window is beginning.

### Phase 2: Database Migration (If Applicable)
This is often the most high-risk part of the deployment.
- **Execute Scripts:** Run the pre-planned migration scripts in the correct order.
- **Monitor Progress:** Watch database performance (CPU, locks, replication lag) closely during execution.
- **Validate Success:** After scripts complete, run validation queries to ensure the schema has been altered correctly and data integrity is intact.

### Phase 3: Application Deployment
This involves rolling out the new application code using the strategy defined in the deployment plan. For specific commands and steps, always refer to the runbook.
- **Execute Rollout:** Follow the steps for your chosen pattern (Blue-Green, Rolling, Canary, etc.).
- **Health Check Instances:** As new instances with the new version come online, ensure they pass their health checks and are able to serve traffic.
- **Verify Version:** Confirm that the new version is being served.

### Phase 4: Smoke Testing
Once the application code is deployed, perform a series of quick, critical tests to ensure the system is fundamentally working.
- **Critical Paths:** Test the most important user journeys (e.g., login, search, checkout).
- **Integrations:** Verify that key third-party integrations are functioning.
- **User Experience:** Do a quick visual check to ensure the UI is rendering correctly and there are no obvious Javascript errors.
- **If smoke tests fail, initiate a rollback immediately.**

### Phase 5: Initial Monitoring & Validation (T+0 to T+60 minutes)
This is the critical window to catch immediate problems.
- **Error Rates:** Monitor error rates (5xx, 4xx). A significant spike is the clearest indicator of a problem.
- **Performance Metrics:** Watch key performance indicators (p95/p99 latency, throughput). A major degradation is a red flag.
- **Business Metrics:** Check high-level business metrics (e.g., sign-ups, transactions). A sharp drop indicates a critical, user-facing problem.
- **Log Review:** Tailing the logs can reveal errors that haven't yet impacted high-level metrics.

### Phase 6: Post-Deployment Tasks
Once the release is stable after the initial monitoring period:
- **Update Execution Log:** Document the actual timeline, any issues encountered, and how they were resolved. This is invaluable for the retrospective.
- **Communicate Success:** Notify all stakeholders that the deployment was successful and that the system is stable.
- **Schedule Extended Monitoring:** Plan for regular check-ins over the next 24-48 hours.

This guide provides the "why" and "what" for each phase. The specific "how" (the exact commands) should always come from the deployment plan (runbook) created for the specific release.
