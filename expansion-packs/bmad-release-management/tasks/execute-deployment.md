# Task: Execute Deployment

**Release Management Phase**: Deployment Execution
**Duration**: 1-4 hours (varies by strategy)
**Agent**: Deployment Coordinator
**Difficulty**: High

## Purpose

Execute the deployment plan to safely deploy the release to production. This task follows the detailed runbook created during planning to ensure consistent, predictable deployment.

## Prerequisites

Before starting this task, ensure you have:

- [ ] **Deployment runbook prepared**: Detailed step-by-step plan ready
- [ ] **Quality gates passed**: Release approved for deployment
- [ ] **Deployment team assembled**: All required people available
- [ ] **Infrastructure access verified**: Credentials working
- [ ] **Backup created**: Database/config backup complete
- [ ] **Communication channels active**: Slack, status page ready
- [ ] **Monitoring dashboards open**: All metrics visible
- [ ] **Deployment checklist available**: `checklists/deployment-checklist.md`

## Step-by-Step Process

### Phase 1: Pre-Deployment (30-60 minutes before)

#### 1.1 Assemble Team

Get everyone on the same communication channel:
- **Deployment Lead**: Coordinating
- **Technical Executor**: Ready to run commands
- **Monitoring Observer**: Watching dashboards
- **QA Validator**: Ready to test
- **Communication Coordinator**: Ready to send updates

**Communication**: "🚀 Deployment team assembled. Beginning pre-deployment checks."

#### 1.2 Final Production Health Check

Verify production is healthy before starting:

```bash
# Check all services healthy
curl https://api.example.com/health

# Check error rates
# Review monitoring dashboard

# Check traffic levels
# Ensure no unusual spikes
```

**Verify**:
- [ ] All services responding
- [ ] Error rates normal (<0.5%)
- [ ] Response times normal
- [ ] No ongoing incidents
- [ ] Traffic levels predictable

**If production unhealthy**: Delay deployment, investigate issues

#### 1.3 Create Backup

Create safety net before making changes:

```bash
# Database backup
pg_dump production_db > backup_v2.1.0_$(date +%Y%m%d_%H%M%S).sql

# Verify backup integrity
pg_restore --list backup_v2.1.0_*.sql

# Config backup
cp -r /etc/app/config /backups/config_$(date +%Y%m%d_%H%M%S)
```

**Verify**: Backup completed and can be restored

#### 1.4 Notify Stakeholders

Send deployment start notification:

**Message**:
```
🚀 v2.1.0 Deployment Beginning
Start Time: [Time]
Estimated Duration: [Duration]
Expected Completion: [Time]
Status updates will be posted every 30 minutes.
```

**Channels**: Slack #releases, Email to stakeholders

#### 1.5 Final Go/No-Go Check

Quick team huddle:
- "Any concerns before we start?"
- "Production healthy?"
- "Team ready?"
- "Rollback plan clear?"

**Deployment Lead**: Make final go/no-go decision

---

### Phase 2: Database Migration (if applicable)

Reference `checklists/deployment-checklist.md` for detailed steps.

#### 2.1 Put Application in Maintenance Mode (if needed)

```bash
# Enable maintenance page
kubectl scale deployment app --replicas=0
# or
cf scale app-name -i 0
```

**Communication**: "⚠️ Maintenance mode enabled for database migration"

#### 2.2 Execute Migration Scripts

Run migrations in order:

```bash
# Run first migration
psql -f 001_add_oauth_tokens_table.sql

# Verify success
# Check migration table or run validation query

# Run second migration
psql -f 002_add_user_preferences_column.sql

# Continue for all migrations...
```

**For each migration**:
- Execute script
- Verify success (check return code, row counts)
- Run validation query
- Log completion time

#### 2.3 Validate Migrations

```sql
-- Verify new columns exist
SELECT column_name FROM information_schema.columns
WHERE table_name = 'users';

-- Check data integrity
SELECT COUNT(*) FROM users WHERE email_address IS NULL;

-- Verify indexes created
SELECT indexname FROM pg_indexes WHERE tablename = 'users';
```

**Verify**: All expected schema changes present, data intact

#### 2.4 Check Database Health

```bash
# Check connection pool
# Check replication lag
# Check slow queries
```

**Verify**: Database performing normally

---

### Phase 3: Application Deployment

Execute deployment using chosen pattern.

#### Option A: Blue-Green Deployment

```bash
# Step 1: Deploy to Green environment
# Deploy new version to green
kubectl apply -f k8s/green-deployment.yaml

# Step 2: Health check green
while ! curl -f https://green.example.com/health; do
  sleep 5
done

# Step 3: Smoke test green
./scripts/smoke-test.sh green.example.com

# Step 4: Switch traffic to green
kubectl patch service app-service -p '{"spec":{"selector":{"version":"green"}}}'

# Step 5: Monitor for 10 minutes
# Watch metrics closely

# Step 6: If stable, mark blue as standby
# Keep blue running for quick rollback
```

#### Option B: Rolling Deployment

```bash
# Deploy to first batch (25% of instances)
kubectl set image deployment/app app=myapp:v2.1.0

# Wait for first batch to be healthy
kubectl rollout status deployment/app

# Monitor first batch for 10 minutes
# Check error rates, response times

# Continue rolling deployment
# Kubernetes will automatically continue
# or manually trigger next batch

# Verify all pods updated
kubectl get pods -l app=myapp -o wide
```

#### Option C: Canary Deployment

```bash
# Deploy canary (single instance)
kubectl apply -f k8s/canary-deployment.yaml

# Route 5% traffic to canary
kubectl apply -f k8s/canary-service.yaml

# Monitor canary for 30 minutes
# Check error rates, performance

# If healthy, increase to 25%
kubectl scale deployment canary --replicas=3

# Continue gradual rollout: 25% → 50% → 100%

# Once at 100%, remove old version
kubectl delete deployment app-v2.0.0
```

**After deployment**:
- Verify all instances running new version
- Check health endpoints
- Verify no old version instances remain

---

### Phase 4: Smoke Testing (15-30 minutes)

Reference `checklists/deployment-checklist.md` Phase 4.

#### 4.1 Test Critical Paths

**Authentication**:
```bash
# Test login
curl -X POST https://api.example.com/auth/login \
  -d '{"email":"test@example.com","password":"test"}'
```

**Core Feature #1**: _________________
- [ ] Test manually in browser/app
- [ ] Verify functionality works
- [ ] Check data persists

**Core Feature #2**: _________________
- [ ] Test manually
- [ ] Verify works

**Core Feature #3**: _________________
- [ ] Test manually
- [ ] Verify works

#### 4.2 Test Integrations

- [ ] Email delivery working
- [ ] Payment processing working (test mode)
- [ ] External APIs responding
- [ ] File uploads working

#### 4.3 Check for Obvious Issues

- [ ] No JavaScript errors in browser console
- [ ] Pages loading correctly
- [ ] No broken images or styles
- [ ] Mobile rendering correct

**If smoke tests fail**: Initiate rollback immediately

---

### Phase 5: Monitoring & Validation (30-60 minutes)

#### 5.1 Monitor Error Rates (First 15 minutes - Critical)

Watch closely for elevated errors:

```
Baseline: 0.1% error rate
Current: ___% error rate

4xx errors: ___ (normal: ≤50/min)
5xx errors: ___ (normal: ≤5/min)
Exceptions: ___ (normal: ≤10/min)
```

**Alert thresholds**:
- Error rate >0.5%: Investigate
- Error rate >2%: Consider rollback
- Error rate >5%: Immediate rollback

#### 5.2 Check Performance Metrics (First 15 minutes)

```
Response Time (p95):
Baseline: 450ms
Current: ___ms
Change: ___% (acceptable if <20% increase)

Response Time (p99):
Baseline: 900ms
Current: ___ms

Throughput:
Baseline: 120 req/s
Current: ___ req/s
```

**Alert thresholds**:
- Response time >2x baseline: Investigate
- Throughput dropped >30%: Investigate

#### 5.3 Monitor Business Metrics (First 30 minutes)

```
Sign-ups per hour:
Baseline: 50/hour
Current: ___/hour

Conversion rate:
Baseline: 3.2%
Current: ___%

Transaction success rate:
Baseline: 99.5%
Current: ___%
```

**Alert thresholds**:
- Business metric drops >20%: Investigate
- Transaction success <95%: Consider rollback

#### 5.4 Review Logs (Ongoing)

```bash
# Check application logs
kubectl logs -f deployment/app --tail=100

# Look for:
# - New error patterns
# - Warning messages
# - Stack traces
# - Failed requests
```

**Red flags**:
- Repeated exceptions
- Database connection errors
- External API timeouts
- Memory warnings

#### 5.5 Hourly Check-ins (First 4 hours)

Every hour, review:
- Error rates (still normal?)
- Performance metrics (stable?)
- Business metrics (trending correctly?)
- User reports (support tickets?)

**Communication**: Post update every hour:
```
"✅ Deployment +1 hour update:
- Error rate: 0.08% (normal)
- Response time p95: 420ms (improved)
- No incidents reported
- Continuing monitoring..."
```

---

### Phase 6: Feature Enablement (if using feature flags)

#### 6.1 Enable for Internal Users (5%)

```bash
# Set feature flag
curl -X POST https://api.example.com/admin/flags \
  -d '{"flag":"oauth_auth","enabled":true,"percentage":5,"target":"internal"}'
```

#### 6.2 Monitor Internal Usage

Watch metrics for internal users:
- Are they using the feature?
- Any errors specific to new feature?
- Feedback positive?

Wait 1-4 hours before expanding.

#### 6.3 Gradual Expansion

- Day 1: 5% (internal)
- Day 2: 25% (beta users)
- Day 5: 50% (half of users)
- Day 7: 100% (all users)

At each phase:
- Monitor metrics
- Collect feedback
- Confirm stability before expanding

---

### Phase 7: Post-Deployment Tasks (15-30 minutes)

#### 7.1 Update Execution Log

Document what happened:
```
Deployment Timeline:
- Pre-deployment: 14:00-14:30 (30 min)
- Database migration: 14:30-14:45 (15 min)
- Application deployment: 14:45-15:15 (30 min)
- Smoke testing: 15:15-15:30 (15 min)
- Monitoring: 15:30-16:30 (60 min)
Total: 2.5 hours

Issues Encountered:
1. Migration took 5 min longer than expected (large table)
   Resolution: Normal, completed successfully

Deviations from Plan:
- None

Rollback Triggered: No
```

#### 7.2 Send Completion Notification

**Message**:
```
✅ v2.1.0 Deployment Complete

Deployment Status: Successful
Completion Time: [Time]
Duration: [Actual time]

All systems healthy:
- Error rate: 0.08% (normal)
- Response time p95: 420ms (baseline: 450ms)
- All smoke tests passed

Continuing monitoring for next 24 hours.

What's New: [Link to release notes]

Thank you to the deployment team! 🎉
```

**Channels**: Slack #releases, Email to stakeholders, Status page

#### 7.3 Update Documentation

- [ ] Mark release as deployed in tracker
- [ ] Update release plan execution log
- [ ] Tag git commit with version
- [ ] Update status page
- [ ] Close deployment incident/ticket

#### 7.4 Schedule Extended Monitoring

Set up check-ins:
- +4 hours: Review metrics
- +24 hours: Full health check
- +48 hours: Final assessment
- +3 days: Retrospective

---

## Rollback Decision Points

Be ready to rollback if:

**Immediate Rollback (no discussion)**:
- Error rate >5%
- Core feature completely broken
- Data corruption detected
- Production completely down

**Discuss Rollback**:
- Error rate 1-5%
- Performance degraded >50%
- Business metrics down >20%
- Multiple user complaints

**Continue with Monitoring**:
- Error rate <1%
- Minor issues with workarounds
- Performance within acceptable range
- User feedback generally positive

**If initiating rollback**: Stop immediately, follow `rollback-release.md`

---

## Expected Outputs

At the end of this task, you should have:

1. **Successful Deployment**: Application running new version
2. **Execution Log**: Documented timeline and issues
3. **Smoke Test Results**: All critical paths verified
4. **Monitoring Data**: First hour metrics collected
5. **Completion Notification**: Stakeholders informed
6. **Updated Release Plan**: Execution section filled in
7. **Extended Monitoring Scheduled**: Follow-up check-ins planned

## Common Challenges & Solutions

### Challenge: "Error rate spiked during deployment"

**Solutions**:
- Check if errors are from new code or deployment process
- Review error messages for patterns
- If new code: consider rollback
- If transient: wait and monitor

### Challenge: "Smoke tests failing"

**Solutions**:
- Rollback immediately
- Don't wait to see if it resolves
- Bad deployments get worse, not better

### Challenge: "Performance degraded significantly"

**Solutions**:
- Check for missing indexes
- Review new code for performance issues
- If >50% degradation: rollback
- If <50%: monitor and create hotfix plan

### Challenge: "Database migration took much longer than expected"

**Solutions**:
- Communicate extended maintenance window
- Don't interrupt running migration
- Monitor database health
- Plan better next time (test on production-sized data)

## Success Indicators

You'll know this task was successful when:

✅ **Deployment completed**: All instances running new version
✅ **No rollback needed**: Made it through monitoring period
✅ **Smoke tests passed**: All critical functionality works
✅ **Metrics healthy**: Error rates, performance normal
✅ **No incidents**: No production issues
✅ **Team confident**: Deployment went smoothly
✅ **Stakeholders informed**: Clear communication throughout

## Related Resources

- **Deployment Checklist**: `checklists/deployment-checklist.md` - Detailed execution steps
- **Deployment Patterns**: `data/deployment-patterns.md` - Pattern-specific guidance
- **Release Plan**: `templates/release-plan.md` - Where to document execution

## Next Tasks

After successful deployment:
→ **monitor-release.md** - Continue monitoring for 24-48 hours
→ **rollback-release.md** - If issues detected (hope you don't need this!)
→ **conduct-retrospective.md** - Learn from the deployment (2-3 days after)
