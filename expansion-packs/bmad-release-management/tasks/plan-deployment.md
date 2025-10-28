# Task: Plan Deployment

**Release Management Phase**: Deployment Planning
**Duration**: 30-60 minutes
**Agent**: Deployment Coordinator
**Difficulty**: Medium-High

## Purpose

Create a detailed, step-by-step deployment plan that ensures safe, predictable deployment to production. This plan serves as the runbook that the deployment team will follow during execution.

## Prerequisites

Before starting this task, ensure you have:

- [ ] **Release scope finalized**: Know what's being deployed
- [ ] **Quality gates passed**: Release approved for deployment
- [ ] **Infrastructure access**: Credentials and permissions verified
- [ ] **Deployment pattern chosen**: Blue-Green, Canary, Rolling, etc.
- [ ] **Database changes identified**: Migrations documented
- [ ] **Target deployment window**: Date and time confirmed
- [ ] **Deployment patterns knowledge**: Refer to `data/deployment-patterns.md`

## Step-by-Step Process

### Phase 1: Select Deployment Strategy (10-15 minutes)

#### 1.1 Assess Release Characteristics

Evaluate the release to choose appropriate strategy:

**Risk Level**:
- High risk: Breaking changes, major refactor, significant features
- Medium risk: New features, moderate changes
- Low risk: Bug fixes, minor updates, hotfix

**User Impact**:
- Critical: Authentication, payments, core features
- Moderate: Secondary features, enhancements
- Low: Internal tools, minor improvements

**Rollback Complexity**:
- Complex: Database schema changes, data migrations
- Moderate: Application code only, backward compatible
- Simple: Feature flags, configuration changes

#### 1.2 Choose Deployment Pattern

Based on assessment, select pattern from `data/deployment-patterns.md`:

**Blue-Green Deployment** - Best for:
- ✅ High-risk releases requiring instant rollback
- ✅ Breaking changes
- ✅ When you can afford 2x infrastructure
- ⏱️ Rollback time: Seconds

**Canary Deployment** - Best for:
- ✅ Gradual rollout desired
- ✅ Large user base (meaningful sample sizes)
- ✅ High-risk changes that need validation
- ⏱️ Rollback time: Minutes

**Rolling Deployment** - Best for:
- ✅ Standard releases
- ✅ Backward-compatible changes
- ✅ Cost-conscious (no extra infrastructure)
- ⏱️ Rollback time: 10-30 minutes

**Feature Flags** - Best for:
- ✅ Decoupling deployment from release
- ✅ A/B testing
- ✅ Instant rollback capability
- ⏱️ Rollback time: Seconds

**Recreate (All-at-Once)** - Best for:
- ✅ Internal tools, dev/staging environments
- ✅ Acceptable downtime window
- ✅ Simple architecture
- ⏱️ Rollback time: 5-15 minutes

Document chosen pattern and rationale in release plan.

### Phase 2: Plan Database Migrations (15-20 minutes)

#### 2.1 List All Database Changes

Identify all schema changes:

```
Migration Scripts:
- 001_add_oauth_tokens_table.sql
- 002_add_user_preferences_column.sql
- 003_create_index_on_email.sql
```

For each migration:
- **Type**: Schema change, data migration, index creation
- **Estimated duration**: Seconds, minutes, hours?
- **Reversibility**: Can it be rolled back?
- **Risk level**: High, medium, low

#### 2.2 Choose Migration Strategy

Refer to `data/deployment-patterns.md` for migration patterns:

**For Breaking Schema Changes** (Use Expand-Contract):

**Phase 1: Expand** (This release):
```sql
-- Add new column alongside old
ALTER TABLE users ADD COLUMN email_address VARCHAR(255);
-- Backfill data
UPDATE users SET email_address = email WHERE email_address IS NULL;
```
Application writes to both columns.

**Phase 2: Migrate** (Next release):
Application reads from new column, writes to both.

**Phase 3: Contract** (Release after):
```sql
-- Remove old column
ALTER TABLE users DROP COLUMN email;
```

**For Backward-Compatible Changes**:
```sql
-- Can deploy immediately
ALTER TABLE users ADD COLUMN phone VARCHAR(20);
CREATE INDEX idx_users_email ON users(email);
```

**For Data Migrations**:
```sql
-- Run as separate step before app deployment
-- Include progress tracking for large datasets
UPDATE users SET status = 'active' WHERE status IS NULL;
```

#### 2.3 Plan Migration Execution Order

Sequence migrations:
1. Backward-compatible schema changes (add columns, tables)
2. Data migrations (update/backfill data)
3. Index creation (can run after deployment in background)
4. Application deployment
5. Forward-only changes (remove old columns - next release)

Document execution order and timing.

#### 2.4 Create Rollback Plan for Migrations

For each migration, document rollback:

**Reversible Migrations**:
```sql
-- UP
ALTER TABLE users ADD COLUMN phone VARCHAR(20);

-- DOWN (rollback)
ALTER TABLE users DROP COLUMN phone;
```

**Irreversible Migrations** (data loss risk):
```sql
-- UP
ALTER TABLE users DROP COLUMN legacy_field;

-- DOWN - CANNOT ROLLBACK WITHOUT DATA LOSS
-- Must restore from backup
```

Mark irreversible migrations clearly: ⚠️ DATA LOSS RISK

### Phase 3: Define Deployment Phases (10-15 minutes)

#### 3.1 Create Phase-by-Phase Plan

Break deployment into discrete phases:

**Example Deployment Plan**:

**Phase 1: Pre-Deployment (30 minutes)**
1. Create database backup (5 min)
2. Verify backup integrity (5 min)
3. Notify stakeholders deployment starting (2 min)
4. Health check all production instances (3 min)
5. Scale up infrastructure if needed (10 min)
6. Feature flags set to OFF for new features (5 min)

**Phase 2: Database Migration (15 minutes)**
1. Put application in maintenance mode (if needed)
2. Run migration scripts in order
3. Validate migration success
4. Run data integrity checks
5. Verify replication caught up

**Phase 3: Application Deployment (30 minutes)**
- Deploy using chosen pattern (Blue-Green, Rolling, etc.)
- Health check after each step
- Verify new version running

**Phase 4: Smoke Testing (15 minutes)**
1. Test user authentication
2. Test core feature #1
3. Test core feature #2
4. Test core feature #3
5. Verify database connectivity

**Phase 5: Monitoring (60 minutes)**
1. Watch error rates (first 30 min)
2. Check performance metrics
3. Monitor business metrics
4. Review logs for anomalies

Total estimated time: 2.5 hours

#### 3.2 Add Verification Steps

After each phase, add verification:
- [ ] Health endpoints returning 200 OK
- [ ] No errors in logs
- [ ] Metrics within normal range
- [ ] Team confirmation to proceed

Create "pause points" where team decides to continue or rollback.

### Phase 4: Plan Feature Flag Configuration (5-10 minutes)

If using feature flags:

#### 4.1 List All Feature Flags

```
Feature Flags in This Release:
- oauth_authentication: OFF (will enable gradually)
- new_dashboard_ui: OFF (will enable for beta users)
- experimental_search: OFF (A/B test)
```

#### 4.2 Plan Rollout Strategy

For each flag:

**oauth_authentication**:
- Deploy: OFF (0% users)
- Day 1: Enable for internal users (5%)
- Day 2: Enable for beta users (25%)
- Day 5: Enable for all users (100%)
- Day 7: Remove flag from code

Document rollout schedule and criteria for advancing.

### Phase 5: Create Rollback Procedures (10-15 minutes)

#### 5.1 Define Rollback Triggers

List conditions that require rollback:

**Automatic Rollback Triggers**:
- Error rate >5% for >5 minutes
- Response time p95 >2x baseline
- Core feature completely broken
- Data corruption detected

**Manual Rollback Triggers**:
- Significant user complaints
- Business metrics drop >20%
- Critical bug discovered
- Leadership decision

#### 5.2 Document Rollback Steps

Create detailed rollback procedure for chosen deployment pattern:

**Blue-Green Rollback**:
```
1. Switch load balancer back to blue environment
2. Verify traffic routed to old version
3. Confirm error rates dropped
4. Keep green environment for debugging
5. Estimated time: 2 minutes
```

**Rolling Rollback**:
```
1. Stop deployment of new version
2. Roll back instances in reverse order
3. Verify each batch returns to old version
4. Confirm full rollback
5. Estimated time: 15 minutes
```

**Feature Flag Rollback**:
```
1. Set feature flag to 0% (OFF)
2. Verify users seeing old behavior
3. Monitor for recovery
4. Estimated time: 30 seconds
```

**Database Rollback** (if migrations were breaking):
```
⚠️ DANGEROUS - DATA LOSS POSSIBLE
1. Stop application
2. Run down migration scripts
3. Verify schema reverted
4. Redeploy old application version
5. Test functionality
6. Estimated time: 30+ minutes
```

#### 5.3 Assign Rollback Decision Maker

Specify who can trigger rollback:
- **Primary**: Release Manager
- **Backup**: On-call Engineer
- **Escalation**: VP Engineering

Document decision criteria and communication process.

### Phase 6: Plan Communications (5 minutes)

#### 6.1 Create Communication Timeline

**T-24 hours**: "Deployment scheduled for [date/time]"
- Audience: Internal stakeholders
- Channel: Email, Slack

**T-1 hour**: "Deployment beginning in 1 hour"
- Audience: Engineering, Product, Support
- Channel: Slack

**T-0**: "🚀 Deployment starting now"
- Audience: All stakeholders
- Channel: Slack #releases

**T+30 min**: "Deployment progress update"
- Audience: Stakeholders
- Channel: Slack

**T+2 hours**: "✅ Deployment complete, monitoring"
- Audience: All stakeholders
- Channel: Email, Slack

**If Rollback**: "⚠️ Initiating rollback due to [reason]"
- Audience: All stakeholders immediately
- Channel: Slack, Email, Status page

#### 6.2 Prepare Message Templates

Draft messages in advance:
```
Success message:
"✅ v2.1.0 deployed successfully. All systems healthy.
Monitoring for next 24 hours. Thank you team!"

Rollback message:
"⚠️ Initiating rollback of v2.1.0 due to [reason].
Estimated rollback time: [X] minutes. Will update shortly."
```

### Phase 7: Assign Roles and Responsibilities (5 minutes)

#### 7.1 Define Team Roles

**Deployment Lead**: ____________
- Overall coordination
- Go/no-go decisions
- Communication

**Technical Executor**: ____________
- Runs deployment commands
- Executes migration scripts
- Manages infrastructure

**Monitoring Observer**: ____________
- Watches dashboards
- Calls out anomalies
- Tracks metrics

**Communication Coordinator**: ____________
- Sends updates
- Manages status page
- Coordinates with support

**QA Validator**: ____________
- Runs smoke tests
- Verifies functionality
- Reports issues

#### 7.2 Confirm Team Availability

Verify all required people are available during deployment window:
- [ ] Deployment Lead confirmed
- [ ] Technical Executor confirmed
- [ ] Monitoring Observer confirmed
- [ ] Backup engineer identified
- [ ] On-call coverage arranged

### Phase 8: Finalize and Document (5 minutes)

#### 8.1 Create Deployment Runbook

Compile all information into single runbook document:

```markdown
# Deployment Runbook: v2.1.0

## Deployment Information
- **Date**: [Date]
- **Time**: [Start time] - [End time]
- **Pattern**: Blue-Green
- **Estimated Duration**: 2.5 hours
- **Lead**: [Name]

## Team
- Lead: [Name]
- Executor: [Name]
- Monitor: [Name]
- QA: [Name]

## Pre-Deployment Checklist
- [ ] [Steps from Phase 1]

## Phase 1: Pre-Deployment
[Detailed steps with commands]

## Phase 2: Database Migration
[Detailed steps with commands]

[... all phases ...]

## Rollback Procedure
[Detailed rollback steps]

## Communication Plan
[Message templates and timeline]
```

#### 8.2 Review with Team

Share runbook with deployment team:
- Walk through each phase
- Clarify any unclear steps
- Practice rollback procedure mentally
- Get team buy-in

#### 8.3 Update Release Plan

Add deployment plan to release plan document:
- Deployment strategy and rationale
- Phase-by-phase steps
- Rollback procedures
- Team assignments
- Communication plan

## Expected Outputs

At the end of this task, you should have:

1. **Deployment Runbook**: Step-by-step execution guide
2. **Chosen Deployment Pattern**: Strategy with rationale
3. **Database Migration Plan**: Sequenced, timed, with rollback
4. **Phase-by-Phase Steps**: Clear instructions for each phase
5. **Verification Checklist**: What to check at each step
6. **Rollback Procedures**: Detailed revert steps
7. **Feature Flag Plan**: Rollout strategy (if applicable)
8. **Communication Timeline**: When/what/who to notify
9. **Team Assignments**: Roles and responsibilities
10. **Updated Release Plan**: Deployment section complete

## Common Challenges & Solutions

### Challenge: "Deployment pattern unclear for our architecture"

**Solutions**:
- Review `data/deployment-patterns.md` for guidance
- Start with Rolling deployment (most common)
- Consider Blue-Green for first major release
- Use Feature Flags to reduce deployment risk

### Challenge: "Database migrations are complex"

**Solutions**:
- Use expand-contract pattern for breaking changes
- Test migrations in staging first
- Create data validation queries
- Consider deploying migrations separately from application
- Have DBA review migration plan

### Challenge: "Rollback plan unclear"

**Solutions**:
- Test rollback in staging environment
- Document every rollback step explicitly
- Identify point of no return (usually data migrations)
- Practice rollback procedure with team
- Have backup plan if primary rollback fails

### Challenge: "Not sure how long deployment will take"

**Solutions**:
- Time each phase in staging
- Add 50% buffer for production
- Plan for best case and worst case
- Have backup deployment window
- Communicate time estimates to stakeholders

### Challenge: "Team not available for deployment window"

**Solutions**:
- Schedule deployment during business hours
- Get backup engineers identified
- Consider automated deployment
- Use multiple smaller deployment windows
- Reschedule if key people unavailable

## Success Indicators

You'll know this task was successful when:

✅ **Comprehensive runbook**: Every step documented
✅ **Clear deployment pattern**: Strategy chosen and justified
✅ **Database migrations planned**: Sequenced with rollback
✅ **Rollback procedures defined**: Team knows how to revert
✅ **Team aligned**: Everyone understands their role
✅ **Time estimated**: Realistic deployment duration
✅ **Communications planned**: Messages drafted
✅ **Confidence high**: Team feels prepared to execute

## Related Resources

- **Deployment Patterns**: `data/deployment-patterns.md` - Strategy guide
- **Deployment Checklist**: `checklists/deployment-checklist.md` - Execution steps
- **Release Plan Template**: `templates/release-plan.md` - Where to document
- **Knowledge Base**: `data/release-management-kb.md` - Best practices

## Next Tasks

After completing deployment planning:
→ **execute-deployment.md** - Execute the plan (deployment day)
→ **rollback-release.md** - If issues arise during deployment
