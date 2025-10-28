# Emergency Rollback Checklist

Use this checklist when a deployment must be reversed due to critical issues. Time is critical—execute methodically but quickly.

## Rollback Decision (⏱️ 5-10 minutes)

### Assess Severity

**Critical Issues (Immediate Rollback)**:
- [ ] **Production outage**: Service completely down
- [ ] **Data corruption**: Data loss or integrity issues
- [ ] **Security breach**: Active security vulnerability
- [ ] **Error rate >5x baseline**: Overwhelming error volume
- [ ] **Complete feature failure**: Core functionality broken
- [ ] **Cascading failures**: System instability spreading

**High Issues (Evaluate Rollback)**:
- [ ] **Partial outage**: Some users affected
- [ ] **Performance degradation >50%**: Severe slowness
- [ ] **Key business metrics down >20%**: Significant impact
- [ ] **Payment processing issues**: Revenue impact
- [ ] **Third-party integration failures**: External dependencies broken

**Medium Issues (Consider Hotfix Instead)**:
- [ ] **Minor feature issues**: Non-critical bugs
- [ ] **Performance degradation <50%**: Noticeable but tolerable
- [ ] **Isolated user reports**: Affecting small user segment
- [ ] **Cosmetic/UI issues**: No functional impact

### Decision Criteria

- [ ] **Issue impact assessed**: Severity understood
- [ ] **Affected user count estimated**: Scope of impact known
- [ ] **Business impact quantified**: Revenue/reputation cost
- [ ] **Hotfix timeframe estimated**: Can we fix forward quickly? (<2 hours)
- [ ] **Rollback risk assessed**: Will rollback make things worse?

### Rollback Decision

**ROLLBACK IF**:
- Critical issue affecting >10% of users
- No hotfix available within 2 hours
- Rollback risk is acceptable
- Leadership approval obtained (for critical decisions)

**HOTFIX IF**:
- Issue is fixable within 1-2 hours
- Fix is low-risk
- Issue is contained/not spreading

---

## Pre-Rollback (⏱️ 5-10 minutes)

### Communication

- [ ] **Incident declared**: Create incident channel (Slack, Teams, etc.)
- [ ] **Incident commander assigned**: Single decision maker
- [ ] **Rollback decision announced**: "🚨 INITIATING ROLLBACK" to team
- [ ] **Stakeholders notified**: Leadership, product, support informed
- [ ] **Status page updated**: "Investigating issues" message posted
- [ ] **Customer communication prepared**: Draft user-facing message

### Team Assembly

- [ ] **Deployment team assembled**: All hands on deck
- [ ] **On-call engineers alerted**: Additional support available
- [ ] **Database admin available** (if DB changes): DBA on standby
- [ ] **Roles assigned**:
  - [ ] Rollback executor
  - [ ] Monitoring observer
  - [ ] Communication coordinator
  - [ ] Incident scribe (documenting)

### Preparation

- [ ] **Previous version identified**: Know exact version to rollback to
- [ ] **Rollback procedure reviewed**: Team knows the steps
- [ ] **Backup verified**: Database backup available if needed
- [ ] **Monitoring dashboards open**: All metrics visible
- [ ] **Runbook accessible**: Rollback steps documented

---

## Rollback Execution

### Pattern-Specific Rollback

Choose the appropriate rollback method based on your deployment pattern:

---

#### Option A: Blue-Green Rollback (⏱️ 1-5 minutes)

- [ ] **Switch traffic back to blue**: Update load balancer/DNS
- [ ] **Verify traffic switched**: Confirm old version receiving traffic
- [ ] **Green environment isolated**: New version stopped receiving traffic
- [ ] **Blue environment healthy**: Old version responding
- [ ] **DNS propagated** (if using DNS switch): Changes propagated

**Rollback Time**: Seconds to minutes

---

#### Option B: Feature Flag Rollback (⏱️ 1-2 minutes)

- [ ] **Disable problematic feature flags**: Toggle off new features
- [ ] **Verify flags disabled**: Confirm new code not executing
- [ ] **User experience verified**: Users seeing old behavior
- [ ] **Flag configuration saved**: Document flag state

**Rollback Time**: Seconds

---

#### Option C: Rolling Rollback (⏱️ 10-30 minutes)

- [ ] **Stop deployment**: Halt any in-progress rollout
- [ ] **Identify instances to rollback**: List all updated instances
- [ ] **Rollback first batch**: Revert first group to old version
- [ ] **Verify batch health**: First batch healthy
- [ ] **Continue rolling back**: Proceed through remaining batches
- [ ] **All instances reverted**: Confirm all running old version

**Rollback Time**: 10-30 minutes

---

#### Option D: Canary Rollback (⏱️ 1-5 minutes)

- [ ] **Reduce canary traffic to 0%**: Stop routing to new version
- [ ] **Verify traffic stopped**: Confirm no users on new version
- [ ] **Canary instances stopped**: Terminate new version instances
- [ ] **All traffic on stable version**: 100% on old version

**Rollback Time**: Minutes

---

#### Option E: Recreate Rollback (⏱️ 5-15 minutes)

- [ ] **Stop new version**: Terminate all new instances
- [ ] **Deploy old version**: Redeploy previous release
- [ ] **Wait for startup**: Allow instances to initialize
- [ ] **Verify health**: Old version healthy
- [ ] **Traffic restored**: Load balancer routing traffic

**Rollback Time**: 5-15 minutes (with downtime)

---

### Database Rollback (If Needed) (⏱️ 10-60 minutes)

⚠️ **WARNING**: Database rollbacks are risky and may cause data loss. Proceed with extreme caution.

#### Forward-Compatible Migrations (Preferred)

- [ ] **Application rolled back**: Old app code running
- [ ] **Old app compatible with new schema**: Verify compatibility
- [ ] **No schema rollback needed**: Migrations left in place
- [ ] **Data integrity verified**: Spot check data

**Best Case**: No database rollback needed

#### Backward-Incompatible Migrations (Dangerous)

- [ ] **Backup verified**: Recent backup available
- [ ] **Data export created**: Additional safety net
- [ ] **Migration rollback script ready**: Down migration tested
- [ ] **Execute down migration**: Revert schema changes
- [ ] **Verify migration success**: Schema reverted correctly
- [ ] **Data integrity checked**: Run validation queries
- [ ] **Application compatibility verified**: Old app works with old schema

⚠️ **Data Loss Risk**: Any data written after migration may be lost

#### Database Restore from Backup (Last Resort)

- [ ] **Confirm data loss acceptable**: Leadership approval obtained
- [ ] **Backup restore point identified**: Exact backup to restore
- [ ] **Initiate database restore**: Begin restore process
- [ ] **Wait for restore completion**: May take 30-60+ minutes
- [ ] **Verify restore success**: Database operational
- [ ] **Data loss documented**: What data was lost

⚠️ **Critical**: All data after backup point will be permanently lost

---

## Post-Rollback Verification (⏱️ 15-30 minutes)

### System Health

- [ ] **All instances healthy**: No crashed instances
- [ ] **Health checks passing**: All endpoints returning 200
- [ ] **Version confirmed**: Verify old version is running
- [ ] **Error rate normalized**: Errors dropped to baseline
- [ ] **Performance restored**: Response times back to normal
- [ ] **Memory usage normal**: No leaks in old version

### Functionality Testing

- [ ] **Homepage loads**: Main landing page accessible
- [ ] **User login works**: Authentication functional
- [ ] **Core features working**: Critical path tested
- [ ] **API endpoints responding**: Key APIs functional
- [ ] **Database queries working**: Data reads/writes functional
- [ ] **No new errors**: Rollback didn't introduce issues

### Monitoring

- [ ] **Metrics returning to normal**: Error rates, performance improving
- [ ] **No rollback-induced issues**: Rollback itself didn't cause problems
- [ ] **Traffic levels recovering**: Users returning
- [ ] **Business metrics stabilizing**: Conversions resuming

---

## Communication (⏱️ 10-15 minutes)

### Internal Communication

- [ ] **Rollback completion announced**: "✅ Rollback complete" to team
- [ ] **Incident status updated**: Timeline and current state
- [ ] **Engineering team notified**: All engineers aware
- [ ] **Support team updated**: What to tell users
- [ ] **Leadership briefed**: Executives informed

### External Communication

- [ ] **Status page updated**: "Issue resolved, monitoring"
- [ ] **User notification sent**: Apologize and explain (if user-facing)
- [ ] **Social media update** (if needed): Address public complaints
- [ ] **Email to affected users** (if appropriate): Personalized outreach

### Stakeholder Communication

- [ ] **Product leadership informed**: PM, CPO, etc.
- [ ] **Business leadership informed**: CEO, COO, etc. (for major incidents)
- [ ] **Customer success informed**: Proactive outreach to key accounts
- [ ] **Sales team informed** (if user-facing): Prepared for customer questions

---

## Root Cause Analysis Prep (⏱️ 30 minutes)

### Data Collection

- [ ] **Incident timeline documented**: Key events and times
- [ ] **Error logs saved**: Captured logs from failure period
- [ ] **Metrics screenshots saved**: Graphs showing impact
- [ ] **User reports collected**: Support tickets, social media
- [ ] **Code changes identified**: What was in the failed release
- [ ] **Configuration changes documented**: What settings changed

### Preliminary Analysis

- [ ] **Immediate cause identified**: What directly caused the failure
- [ ] **Contributing factors noted**: What made it worse
- [ ] **Why issue wasn't caught**: Why testing didn't detect it
- [ ] **Affected user count estimated**: Scope of impact
- [ ] **Duration calculated**: How long issue lasted
- [ ] **Business impact quantified**: Revenue lost, users affected

---

## Incident Documentation (⏱️ 15 minutes)

### Incident Report (Quick Version)

- [ ] **Incident title**: Clear, descriptive name
- [ ] **Severity level**: P0, P1, P2, etc.
- [ ] **Start time**: When issue began
- [ ] **Detection time**: When we noticed
- [ ] **Resolution time**: When rollback completed
- [ ] **Total downtime**: User-facing impact duration
- [ ] **Affected services**: What was impacted
- [ ] **User impact**: How many users affected
- [ ] **Business impact**: Financial or reputation cost
- [ ] **Rollback decision maker**: Who made the call
- [ ] **Resolution summary**: How we fixed it (rollback)

---

## Follow-Up Actions (Within 24 Hours)

### Immediate Actions

- [ ] **Extended monitoring**: Watch system for next 4-8 hours
- [ ] **On-call coverage extended**: Engineers available for follow-up issues
- [ ] **Hotfix development started** (if applicable): Fix the root cause
- [ ] **Post-mortem scheduled**: Within 24-48 hours
- [ ] **Incident report filed**: Document in incident tracking system

### Prevention Planning

- [ ] **Testing gaps identified**: Why didn't we catch this?
- [ ] **Monitoring gaps identified**: Why didn't we see this sooner?
- [ ] **Process improvements identified**: How to prevent recurrence
- [ ] **Action items created**: Specific, assigned, with due dates

---

## Post-Mortem Preparation (Within 48 Hours)

### Data to Gather

- [ ] **Full incident timeline**: Minute-by-minute account
- [ ] **Root cause analysis**: Five whys or similar technique
- [ ] **Impact analysis**: Technical and business impact
- [ ] **Response timeline**: How quickly we detected and responded
- [ ] **Communication review**: How well we communicated
- [ ] **Team feedback**: What went well, what could improve

### Post-Mortem Attendees

- [ ] **Incident commander**: Led the response
- [ ] **Deployment team**: Who executed rollback
- [ ] **Engineering leadership**: VP Eng, CTO, etc.
- [ ] **Product leadership**: PM, CPO, etc.
- [ ] **Support team representative**: Customer-facing perspective
- [ ] **Anyone else involved**: Observers, helpers

---

## Lessons Learned (Post-Incident)

### Process Improvements

- [ ] **Testing improvements**: Add tests to prevent recurrence
- [ ] **Monitoring improvements**: Add alerts to catch earlier
- [ ] **Deployment improvements**: Process changes to reduce risk
- [ ] **Rollback improvements**: Make rollback faster/easier
- [ ] **Communication improvements**: Better incident communication

### Action Items

- [ ] **Technical debt addressed**: Fix the root cause permanently
- [ ] **Documentation updated**: Capture learnings
- [ ] **Runbooks updated**: Improve rollback procedures
- [ ] **Training scheduled**: Share learnings with team
- [ ] **Preventive measures implemented**: Stop recurrence

---

## Rollback Metrics (For Retrospective)

### Timeline Metrics

- **Time to Detection**: _______ minutes (issue start → detection)
- **Time to Decision**: _______ minutes (detection → rollback decision)
- **Time to Rollback**: _______ minutes (decision → rollback complete)
- **Time to Recovery**: _______ minutes (rollback → full recovery)
- **Total Incident Duration**: _______ minutes (issue start → full recovery)

### Impact Metrics

- **Users Affected**: _______
- **Error Count**: _______
- **Business Impact**: $ _______ (if quantifiable)
- **Support Tickets**: _______

### Response Metrics

- **Team Size**: _______ people involved
- **Communication Timeliness**: ☐ Excellent  ☐ Good  ☐ Needs Improvement
- **Decision Speed**: ☐ Excellent  ☐ Good  ☐ Needs Improvement
- **Execution Speed**: ☐ Excellent  ☐ Good  ☐ Needs Improvement

---

## Rollback Completion Sign-Off

- [ ] **System stable**: Monitoring shows healthy metrics
- [ ] **Users can access service**: Core functionality restored
- [ ] **No ongoing issues**: Incident fully resolved
- [ ] **Communication complete**: All stakeholders informed
- [ ] **Documentation complete**: Incident recorded
- [ ] **Follow-up scheduled**: Post-mortem and fixes planned

---

**Incident Commander**: _________________

**Rollback Completion Time**: _________________

**Final Status**: ☐ Fully Resolved  ☐ Partially Resolved  ☐ Ongoing Issues

**Follow-Up Required**: ☐ Hotfix  ☐ Post-Mortem  ☐ Additional Monitoring

**Notes**:


---

## Remember

**Rollbacks are not failures—they are safety mechanisms.** The goal is to protect users and the business. Every rollback is a learning opportunity to improve our processes, testing, and monitoring.

**Blameless culture**: Focus on processes, not people. We learn and improve together.
