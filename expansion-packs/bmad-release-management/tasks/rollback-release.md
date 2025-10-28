# Task: Rollback Release

**Release Management Phase**: Emergency Response
**Duration**: 5 minutes - 2 hours (varies by pattern)
**Agent**: Deployment Coordinator
**Difficulty**: High

## Purpose

Execute an emergency rollback when a deployed release causes critical production issues. This task provides a step-by-step guide for safely reverting to the previous version while minimizing user impact and data loss.

## Prerequisites

Before starting this task, ensure you have:

- [ ] **Rollback decision made**: Clear trigger and approval
- [ ] **Rollback plan documented**: Steps prepared during planning
- [ ] **Deployment team assembled**: All required people available
- [ ] **Communication channels active**: Ready to notify stakeholders
- [ ] **Backup verified**: Previous version available
- [ ] **Rollback checklist**: `checklists/rollback-checklist.md`

## ⚠️ CRITICAL: When to Rollback

### Immediate Rollback (No Discussion Needed)

- **Production completely down**: Service unavailable
- **Data corruption**: Data integrity compromised
- **Security breach**: Active vulnerability being exploited
- **Error rate >5%**: Overwhelming failures
- **Core feature completely broken**: Authentication, payments, critical functionality

### Discuss Rollback (Team Decision)

- **Error rate 1-5%**: Elevated but not catastrophic
- **Performance degraded >50%**: Severe slowness
- **Business metrics down >20%**: Significant impact
- **Multiple user complaints**: Widespread issues

### Continue Monitoring (Don't Rollback)

- **Error rate <1%**: Minor elevation
- **Minor issues with workarounds**: Manageable problems
- **Performance acceptable**: Within range
- **User feedback generally positive**: Few complaints

---

## Step-by-Step Process

### Phase 1: Decision and Communication (2-5 minutes)

#### 1.1 Assess Severity

Quickly evaluate the situation:

**Critical Indicators**:
- [ ] Error rate: ____% (>5% = critical)
- [ ] Response time: ____ms (>2x baseline = critical)
- [ ] Affected users: ____ (>10% = significant)
- [ ] Core features broken: Yes/No
- [ ] Data integrity issues: Yes/No

#### 1.2 Make Rollback Decision

**Decision Maker**: Release Manager (or On-call Lead if unavailable)

**Document**:
```
Rollback Decision: v2.1.0

Time: [Timestamp]
Decided by: [Name]
Reason: [Specific issue]
Severity: Critical / High / Medium
Affected users: [Estimate]
Alternative considered: [Hotfix / Continue monitoring]
Why rollback chosen: [Rationale]
```

#### 1.3 Declare Incident

Create incident channel and declare emergency:

**Announcement**:
```
🚨 INCIDENT: Initiating rollback of v2.1.0

Reason: [Brief description]
Severity: [P0/P1/P2]
Affected: [User impact]
Action: Rolling back to v2.0.0
ETA: [Time estimate]
Incident lead: [Name]

All hands on deck. Updates every 10 minutes.
```

**Channels**: Slack incident channel, Status page, Email (if critical)

#### 1.4 Assemble Team

Get required people immediately:
- **Incident Commander**: Overall coordination
- **Deployment Lead**: Execute rollback
- **Database Administrator**: Handle database rollback if needed
- **Monitoring Observer**: Watch metrics
- **Communication Coordinator**: Update stakeholders

**Communication**: "Incident team assembled. Beginning rollback."

---

### Phase 2: Execute Rollback

Choose rollback method based on deployment pattern used:

---

#### Option A: Blue-Green Rollback (1-5 minutes)

**Fastest rollback method - seconds to switch**

```bash
# Step 1: Switch traffic back to Blue (old version)
kubectl patch service app-service -p '{"spec":{"selector":{"version":"blue"}}}'

# or with load balancer
aws elbv2 modify-target-group --target-group-arn $TG_ARN \
  --target $BLUE_TARGET

# Step 2: Verify traffic switched
curl https://api.example.com/version
# Should return old version number

# Step 3: Health check old version
kubectl get pods -l version=blue
curl https://api.example.com/health

# Step 4: Confirm users seeing old version
# Check monitoring dashboard

# Step 5: Keep Green environment for debugging
# Don't tear down yet - useful for post-mortem
```

**Verification**:
- [ ] Traffic routed to blue environment
- [ ] Health checks passing
- [ ] Error rate dropped
- [ ] Users can access service

**Rollback Time**: 1-2 minutes

---

#### Option B: Feature Flag Rollback (1-2 minutes)

**Instant rollback - if issue is in flagged feature**

```bash
# Step 1: Disable problematic feature flag
curl -X POST https://api.example.com/admin/flags \
  -d '{"flag":"oauth_auth","enabled":false,"percentage":0}'

# Step 2: Verify flag disabled
curl https://api.example.com/admin/flags/oauth_auth
# Should show: enabled: false

# Step 3: Confirm users see old behavior
# Check user sessions

# Step 4: Monitor for recovery
# Watch error rates drop
```

**Verification**:
- [ ] Feature flag set to OFF (0%)
- [ ] Users seeing old functionality
- [ ] Error rate decreased
- [ ] Service operational

**Rollback Time**: 30 seconds - 1 minute

---

#### Option C: Rolling Rollback (10-30 minutes)

**Gradual rollback - roll back instances in reverse**

```bash
# Step 1: Stop any ongoing deployment
kubectl rollout pause deployment/app

# Step 2: Rollback to previous version
kubectl rollout undo deployment/app

# or manually set old image
kubectl set image deployment/app app=myapp:v2.0.0

# Step 3: Watch rollback progress
kubectl rollout status deployment/app

# Step 4: Verify each instance health
kubectl get pods -l app=myapp

# Step 5: Check all instances rolled back
kubectl describe deployment app | grep Image
```

**Monitor at each stage**:
- Watch error rates as old version takes traffic
- Verify health of rolled-back instances
- Confirm users experiencing relief

**Verification**:
- [ ] All pods running old version
- [ ] Health checks passing
- [ ] Error rate normalized
- [ ] Traffic being served

**Rollback Time**: 10-20 minutes

---

#### Option D: Canary Rollback (1-5 minutes)

**Reduce canary to 0% - if using canary deployment**

```bash
# Step 1: Set canary traffic to 0%
kubectl apply -f k8s/canary-0-percent.yaml

# Step 2: Verify no traffic to new version
# Check monitoring dashboard

# Step 3: Scale down canary instances
kubectl scale deployment canary --replicas=0

# Step 4: Confirm all traffic on stable version
kubectl get svc app-service -o yaml | grep selector
```

**Verification**:
- [ ] 0% traffic to new version
- [ ] 100% traffic to old version
- [ ] Error rate dropped
- [ ] Service stable

**Rollback Time**: 2-5 minutes

---

#### Option E: Recreate Rollback (5-15 minutes)

**Complete redeployment - involves downtime**

```bash
# Step 1: Scale down new version
kubectl scale deployment app --replicas=0

# Step 2: Deploy old version
kubectl apply -f k8s/deployment-v2.0.0.yaml

# Step 3: Wait for instances to start
kubectl rollout status deployment/app

# Step 4: Verify health
kubectl get pods -l app=myapp
curl https://api.example.com/health

# Step 5: Confirm version
curl https://api.example.com/version
```

**Verification**:
- [ ] Old version deployed
- [ ] Instances healthy
- [ ] Service accessible
- [ ] Version confirmed

**Rollback Time**: 5-15 minutes (includes downtime)

---

### Phase 3: Database Rollback (if needed)

⚠️ **DANGEROUS - Only if application rollback insufficient**

#### 3.1 Assess Database Rollback Need

**Questions**:
- Can old application work with new database schema? (expand-contract)
- Were schema changes breaking?
- Is data corrupted?
- Can we avoid database rollback?

**Best Case**: No database rollback needed (forward-compatible migrations)

**Acceptable**: Run down migrations (reversible)

**Last Resort**: Restore from backup (data loss)

#### 3.2 Reversible Migration Rollback

If migrations have down scripts:

```bash
# Stop application first
kubectl scale deployment app --replicas=0

# Run down migrations in reverse order
psql -f migrations/002_add_user_preferences_column_down.sql
psql -f 001_add_oauth_tokens_table_down.sql

# Verify schema rolled back
psql -c "\d users"

# Verify data integrity
psql -c "SELECT COUNT(*) FROM users WHERE email IS NOT NULL"

# Restart old application version
kubectl scale deployment app --replicas=10
```

**Risk**: Data written to new columns may be lost

#### 3.3 Database Restore (Last Resort)

⚠️ **DATA LOSS - All data after backup will be lost**

```bash
# Step 1: Stop application
kubectl scale deployment app --replicas=0

# Step 2: Verify backup
pg_restore --list backup_v2.1.0_20250115_140000.sql

# Step 3: Drop current database
dropdb production_db

# Step 4: Restore backup
createdb production_db
pg_restore -d production_db backup_v2.1.0_20250115_140000.sql

# Step 5: Verify restore
psql -c "SELECT COUNT(*) FROM users"

# Step 6: Restart old application
kubectl scale deployment app --replicas=10
```

**Document**: All data between backup time and now is permanently lost

---

### Phase 4: Verification (5-10 minutes)

#### 4.1 Confirm Application Health

```bash
# All instances healthy
kubectl get pods

# Health checks passing
curl https://api.example.com/health

# Correct version running
curl https://api.example.com/version
```

**Verify**:
- [ ] All instances running
- [ ] Health endpoints returning 200
- [ ] Old version confirmed

#### 4.2 Confirm Error Rate Dropped

Monitor for 5-10 minutes:

```
Time after rollback    Error Rate    Status
+2 minutes             2.1%          Dropping ⬇️
+5 minutes             0.8%          Recovering ⬇️
+10 minutes            0.15%         Normal ✅
```

**Success**: Error rate returns to baseline

**Failure**: Error rate still elevated (issue not caused by release)

#### 4.3 Test Critical Functionality

Quick smoke tests:

- [ ] User can log in
- [ ] Core feature #1 works
- [ ] Core feature #2 works
- [ ] Core feature #3 works
- [ ] Payments processing (if applicable)

#### 4.4 Confirm User Access

**Check**:
- [ ] Users can access service
- [ ] No error pages
- [ ] Functionality working
- [ ] Performance acceptable

---

### Phase 5: Communication (5-10 minutes)

#### 5.1 Internal Update

**Message**:
```
✅ Rollback Complete - v2.1.0 → v2.0.0

Status: Rollback successful
Time: [Duration]
Current version: v2.0.0
Health: All systems operational

Metrics:
- Error rate: 0.12% (normal)
- Response time: 440ms (normal)
- All services healthy

Impact:
- Downtime: [X minutes] or [None]
- Affected users: [Estimate]
- Data loss: [None / Minimal / Described]

Root Cause: [Brief description]
Next Steps: [Post-mortem, hotfix plan]

Thank you team for quick response.
```

**Channels**: Slack incident channel, Email to stakeholders

#### 5.2 External Communication

**Status Page Update**:
```
All Systems Operational

We resolved an issue affecting [service] by reverting
to the previous version. All services are now functioning
normally. We apologize for any inconvenience.

Status: Resolved
Duration: [X minutes]
```

**If significant user impact, send email**:
```
Subject: Service Issue Resolved

Dear [Customer],

We experienced a brief issue with [service] today from
[start time] to [end time]. The issue has been fully
resolved and all services are operating normally.

What happened: [Brief, non-technical explanation]
Impact: [What users experienced]
Resolution: [What we did]

We sincerely apologize for any inconvenience.

[Company] Team
```

#### 5.3 Document Incident

Create incident report:

```markdown
## Incident Report: v2.1.0 Rollback

**Incident ID**: INC-2025-001
**Date**: [Date]
**Severity**: P0 / P1 / P2
**Duration**: [Start] - [End] ([Duration])

### Summary
Brief description of what happened.

### Timeline
14:30 - v2.1.0 deployed successfully
15:15 - Error rate elevated to 3.2%
15:20 - Error rate climbing to 5.1%
15:22 - Rollback decision made
15:23 - Rollback initiated
15:25 - Rollback complete
15:30 - Error rate normal (0.12%)

### Impact
- Users affected: ~15% (estimated 5,000 users)
- Duration: 8 minutes elevated errors
- Downtime: None
- Data loss: None

### Root Cause
[Technical description of what went wrong]

### Resolution
Rolled back to v2.0.0 using blue-green deployment pattern.

### Preventive Measures
1. [Action to prevent recurrence]
2. [Monitoring improvement]
3. [Testing improvement]

### Follow-Up
- [ ] Post-mortem scheduled: [Date]
- [ ] Hotfix plan: [Description]
- [ ] Communication to affected users: [Status]
```

---

### Phase 6: Post-Rollback Actions (30-60 minutes)

#### 6.1 Root Cause Analysis

Investigate what went wrong:

```bash
# Check logs from failed deployment
kubectl logs deployment/app-v2.1.0

# Review error messages
# Identify error patterns
# Find code that caused issues
```

**Quick analysis** (detailed post-mortem later):
- What code change caused the issue?
- Why didn't testing catch it?
- What specific trigger caused failures?

#### 6.2 Plan Hotfix or Re-Release

**Decision Options**:

**Option 1: Hotfix**
- Fix the bug quickly
- Deploy as v2.1.1
- Timeline: Hours to 1 day

**Option 2: Defer Features**
- Remove problematic features
- Re-release as v2.1.1
- Timeline: Days

**Option 3: Investigate & Re-plan**
- Need more time to understand
- Plan v2.2.0 with fixes
- Timeline: Weeks

Document the plan.

#### 6.3 Schedule Post-Mortem

Schedule detailed incident review:
- **When**: Within 24-48 hours
- **Who**: All involved team members
- **Duration**: 60-90 minutes
- **Goal**: Learn and prevent recurrence

#### 6.4 Update Release Plan

Add rollback information to release plan:

```markdown
## Rollback Summary

**Rollback Executed**: Yes
**Trigger Time**: [Time]
**Trigger Reason**: Error rate exceeded 5% (5.1%)
**Rollback Method**: Blue-Green switch
**Rollback Duration**: 3 minutes
**Rollback Success**: Yes

**Impact**:
- Duration: 8 minutes of elevated errors
- Users affected: ~5,000 (15%)
- Downtime: None
- Data loss: None

**Root Cause**: [Brief description]

**Lessons Learned**:
1. [Lesson 1]
2. [Lesson 2]

**Follow-Up Actions**:
- [ ] Post-mortem: [Date]
- [ ] Hotfix plan: [Status]
- [ ] Testing improvements: [Description]
```

---

## Expected Outputs

At the end of this task, you should have:

1. **Successful Rollback**: Service running previous version
2. **Service Restored**: Error rates normalized
3. **Incident Documentation**: Timeline and impact recorded
4. **Communication Sent**: Stakeholders informed
5. **Root Cause Identified**: Understanding of what failed
6. **Hotfix Plan**: Path forward documented
7. **Post-Mortem Scheduled**: Learning session planned
8. **Updated Release Plan**: Rollback section filled in

## Common Challenges & Solutions

### Challenge: "Error rate still high after rollback"

**Possible Causes**:
- Issue wasn't caused by new release
- Database not rolled back (incompatible with old app)
- External dependency failure
- Cascading failure in other services

**Solutions**:
- Verify old version actually deployed
- Check database compatibility
- Investigate external services
- May need additional rollbacks or fixes

### Challenge: "Database can't be rolled back"

**Solutions**:
- Check if old app can work with new schema (expand-contract)
- Consider running migrations in reverse if possible
- Restore from backup only as absolute last resort
- Accept some data loss if necessary for service restoration

### Challenge: "Rollback taking too long"

**Solutions**:
- Ensure automated rollback procedures
- Use faster deployment patterns (Blue-Green)
- Have pre-tested rollback procedures
- Consider partial rollback (rollback just broken component)

### Challenge: "Users already affected, data may be corrupted"

**Solutions**:
- Rollback to stop further damage
- Assess data corruption scope
- Plan data repair strategy
- Communicate transparently to affected users
- Consider individual user data restoration

## Success Indicators

You'll know this task was successful when:

✅ **Service restored**: Application running and accessible
✅ **Error rate normalized**: Metrics back to baseline
✅ **User impact minimized**: Quick resolution
✅ **Clear documentation**: Incident well-recorded
✅ **Team coordinated**: Smooth execution under pressure
✅ **Stakeholders informed**: Clear communication throughout
✅ **Learnings captured**: Prepared for post-mortem
✅ **Path forward clear**: Hotfix or re-release plan ready

## Remember

**Rollbacks are not failures—they are safety mechanisms.**

The ability to rollback quickly is a sign of engineering maturity. Every rollback is a learning opportunity to improve processes, testing, and monitoring.

**Blameless culture**: Focus on processes that failed, not people. Everyone did their best with the information available.

## Related Resources

- **Rollback Checklist**: `checklists/rollback-checklist.md` - Detailed rollback procedures
- **Deployment Patterns**: `data/deployment-patterns.md` - Rollback methods by pattern
- **Knowledge Base**: `data/release-management-kb.md` - Incident response philosophy

## Next Tasks

After rollback:
→ **monitor-release.md** - Monitor rolled-back version stability
→ **conduct-retrospective.md** - Post-mortem to learn from incident
→ Plan hotfix or re-release to address root cause
