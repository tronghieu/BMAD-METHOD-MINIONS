# Task: Monitor Release

**Release Management Phase**: Post-Deployment Monitoring
**Duration**: 24-48 hours (with scheduled check-ins)
**Agent**: Release Manager
**Difficulty**: Medium

## Purpose

To continuously monitor a new release after deployment, ensuring it remains stable and healthy, catching any emergent issues early, and formally declaring the release a success.

## Prerequisites

- The new release has been successfully deployed to production.
- Monitoring dashboards and alerting systems are fully operational.
- The `post-deployment-checklist.md` is available.

## High-Level Process

As the Release Manager, your goal is to orchestrate the post-deployment monitoring process to validate the release's stability. Use the `checklists/post-deployment-checklist.md` for specific verification steps and refer to `data/post-release-monitoring-guide.md` for detailed methodology.

### 1. Intensive Monitoring (First 4 Hours)
- [ ] Assemble the monitoring team (Release Manager, on-call engineer).
- [ ] For the first hour, check key health metrics (error rate, latency, infrastructure) every 15 minutes.
- [ ] For the next three hours, check key metrics every 30-60 minutes.
- [ ] Triage any alerts immediately. If a rollback trigger is met, escalate to the `Deployment Coordinator` and execute the `rollback-release` task.
- [ ] Post hourly status updates to stakeholders.

### 2. Extended Monitoring (4-24 Hours)
- [ ] Schedule check-ins to review metrics every 4 hours.
- [ ] Analyze trends in performance and error rates.
- [ ] Monitor user-reported feedback from support channels and social media.
- [ ] At the 24-hour mark, compile and distribute the **24-Hour Health Report**, including a "Green/Yellow/Red" status.

### 3. Final Assessment (24-48 Hours)
- [ ] Conduct a final health check at the 48-hour mark to confirm sustained stability.
- [ ] Compare the release's metrics against historical data from previous releases.
- [ ] Formally declare the release "Stable" and communicate this to all stakeholders.
- [ ] Transition from the deployment team back to standard on-call monitoring procedures.
- [ ] Schedule the post-release retrospective.

## Expected Outputs

- A series of **hourly status updates** during the intensive monitoring period.
- A comprehensive **24-Hour Health Report**.
- A final **48-Hour Assessment** and declaration of release stability.
- All relevant monitoring data and logs saved for the upcoming retrospective.

## Related Resources
- **Execution Checklist**: `checklists/post-deployment-checklist.md`
- **Methodology Guide**: `data/post-release-monitoring-guide.md`
- **Knowledge Base**: `data/release-management-kb.md`
- **Emergency Procedure**: `tasks/rollback-release.md`
