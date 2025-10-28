# Deployment Execution Checklist

Use this checklist during the actual deployment to production. Follow each step in order and verify completion before proceeding.

## Pre-Deployment (T-60 minutes)

### Team Coordination

- [ ] **Deployment team assembled**: All required people online/available
- [ ] **Communication channel active**: Slack/Teams deployment channel ready
- [ ] **Roles confirmed**:
  - [ ] Deployment lead identified
  - [ ] Technical executor assigned
  - [ ] Monitoring observer assigned
  - [ ] Communication coordinator assigned
- [ ] **Stakeholders notified**: "Deployment starting in 60 minutes" message sent
- [ ] **On-call coverage confirmed**: Engineers available for next 4-8 hours

### Environment Verification

- [ ] **Production health check**: All systems currently healthy
- [ ] **No ongoing incidents**: No active P0/P1 issues
- [ ] **Traffic levels normal**: No unusual spikes or drops
- [ ] **Dependencies healthy**: External services and APIs operational
- [ ] **Database connections healthy**: Connection pools stable
- [ ] **Background jobs stable**: Queue depths normal

### Final Preparations

- [ ] **Backup created**: Database/config backup completed and verified
- [ ] **Backup restoration tested**: Verified backup can be restored
- [ ] **Deployment runbook open**: Step-by-step guide accessible to all
- [ ] **Rollback plan reviewed**: Team knows how to revert
- [ ] **Monitoring dashboards open**: Key metrics visible
- [ ] **Alert channels active**: Notifications routing correctly
- [ ] **Credentials validated**: All necessary access confirmed
- [ ] **Browser cache cleared** (if web app): Testing with fresh state

---

## Deployment Start (T-0)

### Deployment Kickoff

- [ ] **Deployment start announced**: "🚀 Deployment beginning now" message sent
- [ ] **Start time recorded**: Document exact timestamp
- [ ] **Deployment freeze initiated**: No other changes during deployment window
- [ ] **Monitoring intensified**: All eyes on dashboards

---

## Phase 1: Pre-Deployment Tasks

### Feature Flags (If Using)

- [ ] **New features flagged off**: Ensure new code deploys in disabled state
- [ ] **Feature flag config reviewed**: Verify targeting rules
- [ ] **Kill switch tested**: Confirm ability to disable features instantly

### Traffic Management

- [ ] **Maintenance page prepared** (if needed): Ready to show users
- [ ] **Rate limits adjusted** (if needed): Prepared for migration traffic
- [ ] **CDN cache cleared** (if needed): Purged old assets
- [ ] **Load balancer ready**: Health check thresholds reviewed

### Communication

- [ ] **Internal notification sent**: "Deployment in progress" to team
- [ ] **External notification sent** (if user-facing): Status page updated
- [ ] **Support team alerted**: Ready for user inquiries

---

## Phase 2: Database Migrations (If Applicable)

### Pre-Migration

- [ ] **Migration scripts reviewed**: Final review of SQL/migration files
- [ ] **Migration tested in staging**: Validated in production-like environment
- [ ] **Database backup confirmed**: Recent backup available
- [ ] **Replication lag checked**: Replicas in sync with primary
- [ ] **Connection pool increased** (if needed): Extra connections for migration

### Migration Execution

- [ ] **Start migration**: Execute database migration scripts
- [ ] **Monitor migration progress**: Watch for errors or slowness
- [ ] **Verify migration success**: Check migration completed successfully
- [ ] **Validate data integrity**: Run data validation queries
- [ ] **Check indexes created**: Ensure new indexes built
- [ ] **Monitor database performance**: Query times, locks, replication lag

### Post-Migration

- [ ] **Migration logged**: Record completion time and result
- [ ] **Database health verified**: No blocking queries or deadlocks
- [ ] **Replication caught up**: Replicas in sync
- [ ] **Application compatibility**: Old app still works (if rolling deployment)

---

## Phase 3: Application Deployment

### Deployment Pattern: Choose One

#### Option A: Blue-Green Deployment

- [ ] **Green environment deployed**: New version running in green
- [ ] **Green environment smoke tests**: Basic functionality verified
- [ ] **Traffic switched to green**: Load balancer/DNS updated
- [ ] **Green environment monitoring**: Watching for errors
- [ ] **Blue environment on standby**: Ready for instant rollback

#### Option B: Rolling Deployment

- [ ] **First batch deployed**: Update first group of instances
- [ ] **First batch health checked**: New instances healthy
- [ ] **First batch monitored**: No errors in first 5-10 minutes
- [ ] **Second batch deployed**: Update next group
- [ ] **Second batch health checked**: New instances healthy
- [ ] **Continue until complete**: Roll through all batches
- [ ] **All instances healthy**: Final health check

#### Option C: Canary Deployment

- [ ] **Canary instance deployed**: Single instance with new version
- [ ] **5% traffic routed to canary**: Small subset of users
- [ ] **Canary monitored for 30 min**: No elevated errors
- [ ] **25% traffic to canary**: Increase user exposure
- [ ] **25% monitored for 30 min**: Metrics still healthy
- [ ] **50% traffic to canary**: Half of users
- [ ] **50% monitored for 30 min**: Continued stability
- [ ] **100% traffic to new version**: Full rollout complete

### Application Health

- [ ] **Health endpoints responding**: `/health` returns 200 OK
- [ ] **Readiness checks passing**: Application ready for traffic
- [ ] **Startup complete**: All instances fully initialized
- [ ] **No startup errors**: Clean application logs
- [ ] **Memory usage normal**: No memory leaks detected
- [ ] **CPU usage normal**: Processing efficiently

---

## Phase 4: Smoke Testing

### Critical Path Testing

- [ ] **Homepage loads**: Main landing page accessible
- [ ] **User login works**: Authentication functional
- [ ] **Core feature #1 tested**: [Specify your core feature]
- [ ] **Core feature #2 tested**: [Specify your core feature]
- [ ] **Core feature #3 tested**: [Specify your core feature]
- [ ] **API endpoints responding**: Key APIs returning expected data
- [ ] **Database queries working**: Data reads/writes functional

### Integration Testing

- [ ] **Payment processing works** (if applicable): Test transactions
- [ ] **Email sending works** (if applicable): Test email delivery
- [ ] **Third-party integrations work**: External APIs responding
- [ ] **File uploads work** (if applicable): Upload and retrieval functional
- [ ] **Search functionality works** (if applicable): Queries returning results

### User Experience

- [ ] **UI renders correctly**: No broken layouts or styling
- [ ] **No JavaScript errors**: Browser console clean
- [ ] **Images loading**: Assets served correctly
- [ ] **Forms submitting**: User inputs processing
- [ ] **Mobile app works** (if applicable): iOS/Android functional

---

## Phase 5: Monitoring & Validation

### Error Monitoring (15-30 minutes)

- [ ] **Error rate checked**: Not elevated from baseline
- [ ] **Error logs reviewed**: No new critical errors
- [ ] **Exception tracking**: No new exception types
- [ ] **4xx rates normal**: Client errors within expected range
- [ ] **5xx rates normal**: Server errors not elevated

### Performance Monitoring (15-30 minutes)

- [ ] **Response times checked**: p50, p95, p99 within SLA
- [ ] **Throughput verified**: Requests per second as expected
- [ ] **Database query times**: No slow queries introduced
- [ ] **Cache hit rates**: Caching working as expected
- [ ] **Memory usage stable**: No leaks detected
- [ ] **CPU usage normal**: Processing efficiently
- [ ] **Disk I/O normal**: Not excessive reads/writes

### Business Metrics (15-30 minutes)

- [ ] **User sign-ups tracking**: Registration flow working
- [ ] **Transactions processing**: Payment flows functional
- [ ] **Key conversions tracking**: Core KPIs not dropped
- [ ] **User engagement normal**: Activity levels as expected
- [ ] **No unusual drop-offs**: Funnel metrics stable

### Infrastructure Monitoring

- [ ] **Pod/container health**: All replicas running
- [ ] **Load balancer healthy**: Distributing traffic evenly
- [ ] **Auto-scaling working**: Scaling policies triggering correctly
- [ ] **Network latency normal**: No connectivity issues
- [ ] **Queue depths normal**: Background jobs processing

---

## Phase 6: Feature Enablement (If Using Feature Flags)

### Gradual Feature Rollout

- [ ] **Enable for internal users**: 5% rollout to team
- [ ] **Internal feedback collected**: Quick sanity check
- [ ] **Enable for beta users**: 25% rollout to early adopters
- [ ] **Monitor for 1 hour**: Metrics stable
- [ ] **Enable for 50% of users**: Expand rollout
- [ ] **Monitor for 1 hour**: Continued stability
- [ ] **Enable for 100% of users**: Full feature activation

### Feature Validation

- [ ] **New feature accessible**: Users can see/use new functionality
- [ ] **New feature working**: Core functionality operational
- [ ] **Analytics tracking**: Events firing correctly
- [ ] **No feature-specific errors**: New code not throwing errors

---

## Phase 7: Post-Deployment Verification

### Final Checks

- [ ] **All instances updated**: No old versions running
- [ ] **Version verification**: Confirm version number deployed
- [ ] **Configuration applied**: Environment variables correct
- [ ] **Secrets rotated** (if applicable): New credentials active
- [ ] **Old versions removed**: Cleanup of old containers/artifacts
- [ ] **Deployment artifacts saved**: Logs, configs archived

### Documentation

- [ ] **Deployment logged**: Record in release plan document
- [ ] **Timestamp recorded**: Note exact deployment completion time
- [ ] **Issues encountered documented**: Any problems or deviations noted
- [ ] **Resolutions documented**: How issues were addressed

### Communication

- [ ] **Internal success notification**: "✅ Deployment complete" to team
- [ ] **External announcement sent**: Release notes to users
- [ ] **Status page updated**: "All systems operational"
- [ ] **Support team notified**: Deployment complete, watch for inquiries
- [ ] **Stakeholders updated**: Summary email sent

---

## Phase 8: Extended Monitoring

### First 4 Hours

- [ ] **Hourly metric checks**: Error rates, performance, business metrics
- [ ] **Alert monitoring**: Watch for anomalies
- [ ] **User feedback monitoring**: Support tickets, social media, forums
- [ ] **On-call team standing by**: Ready to respond

### First 24 Hours

- [ ] **Scheduled check-ins**: Every 6 hours review metrics
- [ ] **Trending analysis**: Compare hour-over-hour metrics
- [ ] **Cumulative error review**: No concerning patterns emerging
- [ ] **Performance trending**: Response times stable or improving

---

## Rollback Criteria (Trigger Rollback If)

### Critical Issues

- ⚠️ **Error rate >2x baseline**: Elevated 5xx errors
- ⚠️ **Core functionality broken**: Login, checkout, or critical feature down
- ⚠️ **Data integrity issue**: Data corruption or loss detected
- ⚠️ **Security vulnerability**: New security hole introduced
- ⚠️ **Performance degradation >50%**: Unacceptable slowness
- ⚠️ **Cascading failures**: System instability spreading

### Business Impact

- ⚠️ **Key conversions down >20%**: Significant business impact
- ⚠️ **User complaints spiking**: Overwhelming support volume
- ⚠️ **Partner/integration failures**: External dependencies broken
- ⚠️ **Revenue impact**: Payment processing affected

If any rollback criteria met, **immediately initiate rollback procedure** (see rollback-checklist.md).

---

## Deployment Sign-Off

### Deployment Team

- [ ] **Technical lead approval**: Deployment executed successfully
- [ ] **Monitoring team approval**: Metrics look healthy
- [ ] **QA spot-check passed**: Quick validation successful

### Completion

- [ ] **Deployment marked complete**: Status updated in tracking system
- [ ] **Deployment time recorded**: Total time from start to finish
- [ ] **Post-deployment monitoring scheduled**: Next 24-48 hours
- [ ] **Retrospective scheduled** (within 3 days): Learn from deployment

---

**Deployment Lead Signature**: _________________

**Deployment Completion Time**: _________________

**Deployment Status**: ☐ Success  ☐ Success with Issues  ☐ Rolled Back

**Notes/Issues**:
