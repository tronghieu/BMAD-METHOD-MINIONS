# Task: Rollback Release

**Release Management Phase**: Emergency Response
**Duration**: 5 - 60 minutes
**Agent**: Deployment Coordinator
**Difficulty**: High (High-Stress)

## ⚠️ PURPOSE: EMERGENCY PROCEDURE ⚠️

To execute an emergency rollback to restore service as quickly as possible. This task is initiated when a deployment has resulted in a critical production issue. Speed, accuracy, and calm communication are paramount.

## Prerequisites

- A critical rollback trigger has been met (e.g., error rate >5%, data corruption, service outage).
- The decision to roll back has been made by the Incident Commander or Release Manager.
- The `rollback-checklist.md` is available.

## High-Level Process

As the Deployment Coordinator, you are now in an emergency response situation. Your goal is to restore the system to its last known good state. Follow the `checklists/rollback-checklist.md` precisely. Refer to `data/rollback-guide.md` for methodology.

### 1. Declare Incident & Assemble Team (Time: 0-2 minutes)
- [ ] **Declare a SEV-1/P0 Incident.** Use the designated emergency communication channel.
- [ ] Announce that you are initiating a rollback, stating the reason clearly and concisely.
- [ ] Assemble the core incident response team (Incident Commander, DBA, on-call engineer).

### 2. Execute Rollback (Time: 2-30 minutes)
- [ ] **Execute the pre-planned rollback procedure** for the deployment pattern that was used. Follow the steps in the deployment runbook and `rollback-checklist.md` exactly.
- [ ] **Application First:** Always roll back the application code first.
- [ ] **Database Second (ONLY IF NECESSARY):** Do not perform a database rollback unless it is confirmed that the application rollback alone is insufficient. This step is high-risk and requires careful consideration of data loss.

### 3. Verify Service Restoration (Time: 5-15 minutes)
- [ ] As the system comes back online on the previous version, monitor key metrics.
- [ ] **Confirm error rates are dropping** to baseline levels.
- [ ] **Confirm performance metrics are returning** to normal.
- [ ] Perform a quick smoke test of critical functionality.

### 4. Communicate Resolution & Begin Post-Mortem
- [ ] Once the service is stable, communicate the resolution to all stakeholders and update the status page.
- [ ] Document the incident timeline and preliminary root cause.
- [ ] Formally hand off the incident to the Release Manager to schedule a post-mortem.

## Expected Outputs

- A **restored and stable production environment** running the previous software version.
- An initial **incident report** with a timeline, impact analysis, and resolution summary.
- A **post-mortem meeting scheduled** to analyze the root cause and prevent recurrence.

## Related Resources
- **Execution Checklist**: `checklists/rollback-checklist.md`
- **Methodology Guide**: `data/rollback-guide.md`
- **Supporting Data**: `data/deployment-patterns.md` (for pattern-specific rollback steps)
