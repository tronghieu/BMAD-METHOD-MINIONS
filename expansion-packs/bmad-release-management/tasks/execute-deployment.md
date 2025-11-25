# Task: Execute Deployment

**Release Management Phase**: Deployment Execution
**Duration**: 1-4 hours
**Agent**: Deployment Coordinator
**Difficulty**: High

## Purpose

To safely and predictably execute the approved deployment plan (runbook), deploying the new release to production while minimizing risk and downtime.

## Prerequisites

- The **Deployment Plan (Runbook)** for this release is complete, reviewed, and approved.
- The release has passed all quality gates.
- The deployment team is assembled and ready.
- All pre-deployment checks from `checklists/deployment-checklist.md` are complete.

## High-Level Process

As the Deployment Coordinator, your role is to orchestrate the deployment by strictly following the official runbook. Use the `checklists/deployment-checklist.md` for step-by-step execution and refer to `data/deployment-execution-guide.md` for detailed methodology.

### 1. Pre-Deployment Final Checks (T-60 to T-0)
- [ ] Announce the start of the deployment window and assemble the team on the designated communication channel.
- [ ] Perform a final health check of the production environment. **Do not proceed if the system is unhealthy.**
- [ ] Verify the database and configuration backups are complete and valid.
- [ ] Make the final **Go/No-Go** decision with the team.

### 2. Execute the Runbook
- [ ] Follow the deployment plan phase by phase, step-by-step. **Do not deviate from the plan.**
- [ ] Announce the start and completion of each major phase (e.g., "Starting database migrations," "Application deployment complete").
- [ ] **Execute database migrations** as specified in the runbook, verifying success after each script.
- [ ] **Execute application deployment** using the chosen strategy (Blue-Green, Canary, etc.).

### 3. Verify the Deployment
- [ ] Immediately after the deployment, perform all **smoke tests** as documented in the runbook.
- [ ] **If any smoke test fails, initiate the rollback procedure immediately.**
- [ ] Begin the **intensive monitoring** period (the first 60 minutes). Watch error rates, performance metrics, and key business metrics.

### 4. Declare Success or Rollback
- [ ] If the initial monitoring period passes without triggering any rollback criteria, declare the deployment a success.
- [ ] Communicate the successful completion to all stakeholders.
- [ ] Transition to the extended monitoring phase as defined in the `monitor-release` task.
- [ ] If rollback criteria are met at any point, immediately switch to the `rollback-release` task.

### 5. Document Execution
- [ ] Throughout the process, fill out the **Execution Log** in the main release plan document with actual times, any issues encountered, and their resolutions.

## Expected Outputs

- A successful deployment of the new release to production.
- A fully populated **Execution Log** detailing the timeline and events of the deployment.
- Clear communication to all stakeholders regarding the status and outcome of the deployment.

## Related Resources
- **Primary Runbook**: The `deployment-plan.md` created for this specific release.
- **Execution Checklist**: `checklists/deployment-checklist.md`
- **Methodology Guide**: `data/deployment-execution-guide.md`
- **Emergency Procedure**: `tasks/rollback-release.md`
