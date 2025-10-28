# Post-Deployment Verification Checklist

Use this checklist after deployment completes to ensure the release is stable and healthy. This extends beyond initial smoke tests to comprehensive validation over the first 24-48 hours.

## Immediate Verification (T+0 to T+1 Hour)

### System Health

- [ ] **All instances healthy**: No crashed or restarting containers/pods
- [ ] **Health endpoints responding**: All `/health` checks returning 200
- [ ] **Readiness checks passing**: All instances accepting traffic
- [ ] **No memory leaks**: Memory usage stable and within limits
- [ ] **CPU usage normal**: Processing efficiency as expected
- [ ] **Disk space adequate**: No disk space warnings

### Error Rates

- [ ] **5xx error rate normal**: Server errors within baseline (<0.1% typical)
- [ ] **4xx error rate normal**: Client errors not elevated
- [ ] **Exception rate normal**: No new exception types
- [ ] **Error logs reviewed**: No concerning error patterns
- [ ] **Dead letter queues empty**: Failed jobs not accumulating

### Performance Metrics

- [ ] **Response time p50 normal**: Median response time as expected
- [ ] **Response time p95 acceptable**: 95th percentile within SLA
- [ ] **Response time p99 acceptable**: 99th percentile within SLA
- [ ] **Throughput as expected**: Requests per second normal
- [ ] **Database query times normal**: No slow queries introduced
- [ ] **Cache hit rate healthy**: Caching working effectively (>80% typical)

### Business Metrics

- [ ] **User traffic levels normal**: No unexpected drops
- [ ] **Conversion rates stable**: Key funnels performing
- [ ] **Transaction success rate normal**: Payments processing
- [ ] **API usage normal**: Third-party consumers not affected
- [ ] **Feature usage tracking**: New features analytics firing

---

## Extended Monitoring (T+1 to T+4 Hours)

### Trend Analysis

- [ ] **Error rate trending down or stable**: Not climbing over time
- [ ] **Performance metrics stable**: No degradation over time
- [ ] **Memory usage not climbing**: No memory leaks
- [ ] **Database connections stable**: Connection pool not exhausting
- [ ] **Queue depths stable**: Background jobs processing normally

### User Experience

- [ ] **No user complaints**: Support tickets not spiking
- [ ] **Social media monitoring**: No complaints on Twitter/social
- [ ] **Community forums calm**: No widespread issues reported
- [ ] **Mobile app reviews stable**: No 1-star review spike
- [ ] **NPS/satisfaction scores normal**: User sentiment unchanged

### Integration Health

- [ ] **Third-party APIs responding**: External services working
- [ ] **Webhooks delivering**: Outbound notifications sending
- [ ] **Email delivery working**: Transactional emails sending
- [ ] **Payment processing normal**: Stripe/PayPal/etc. working
- [ ] **SMS delivery working** (if applicable): Notifications sending

---

## Full Day Verification (T+4 to T+24 Hours)

### Cumulative Metrics

- [ ] **Total error count acceptable**: Not significantly elevated
- [ ] **No new error patterns**: Consistent with pre-deployment
- [ ] **Performance sustained**: No degradation over 24 hours
- [ ] **Business KPIs met**: Revenue, conversions, engagement on track
- [ ] **User growth maintained**: Sign-ups/activations normal

### Infrastructure

- [ ] **Auto-scaling functioning**: Scales up/down as expected
- [ ] **Load balancing healthy**: Traffic distributed evenly
- [ ] **Database replication healthy**: Replicas in sync
- [ ] **Backup jobs successful**: Scheduled backups running
- [ ] **Log aggregation working**: Logs flowing to centralized system
- [ ] **Monitoring alerts functioning**: Test alert fired successfully

### Security

- [ ] **No security incidents**: No suspicious activity
- [ ] **Authentication working**: Login systems functional
- [ ] **Authorization correct**: Permissions enforced properly
- [ ] **Rate limiting effective**: No API abuse detected
- [ ] **SSL certificates valid**: No cert expiration warnings

---

## Feature-Specific Verification

### New Features (If Added)

- [ ] **Feature accessible**: Users can find and use new functionality
- [ ] **Feature working correctly**: Core functionality operational
- [ ] **Feature analytics tracking**: Events/metrics collecting
- [ ] **Feature performance acceptable**: Not causing slowdowns
- [ ] **Feature errors minimal**: No elevated errors from new code
- [ ] **Feature adoption tracking**: Usage metrics as expected

### Changed Features (If Modified)

- [ ] **Modified functionality working**: Changes implemented correctly
- [ ] **No regressions**: Existing behavior preserved where intended
- [ ] **Performance maintained**: No degradation from changes
- [ ] **User adaptation smooth**: Users adapting to changes

### Removed Features (If Deprecated)

- [ ] **Deprecated features removed cleanly**: No dead code errors
- [ ] **Users transitioned**: Communication about removal received
- [ ] **No broken links**: UI references to removed features cleaned up
- [ ] **Documentation updated**: Help docs reflect removals

---

## Database Verification (If Schema Changed)

### Data Integrity

- [ ] **Data validation queries passed**: Integrity constraints met
- [ ] **No data corruption**: Spot checks show clean data
- [ ] **Indexes created successfully**: Query performance optimal
- [ ] **Foreign keys intact**: Referential integrity maintained
- [ ] **Data migration complete**: All records migrated

### Database Performance

- [ ] **Query performance acceptable**: No slow query log spikes
- [ ] **Connection pool healthy**: Not exhausting connections
- [ ] **Replication lag minimal**: Replicas <1 second behind primary
- [ ] **Table bloat acceptable**: No excessive table growth
- [ ] **Index usage optimal**: Indexes being utilized

---

## Documentation & Communication

### Internal Documentation

- [ ] **Deployment documented**: Release plan updated with execution notes
- [ ] **Issues documented**: Any problems encountered recorded
- [ ] **Resolutions documented**: How issues were addressed
- [ ] **Lessons learned captured**: Quick notes for retrospective

### External Communication

- [ ] **Release announcement published**: Blog post, social media, etc.
- [ ] **Release notes published**: User-facing changelog available
- [ ] **Documentation site updated**: Docs reflect new version
- [ ] **Status page updated**: "All systems operational" status
- [ ] **API clients notified** (if API changed): Third-party developers informed

### Team Communication

- [ ] **Engineering team updated**: Deployment complete notification
- [ ] **Product team updated**: New features live
- [ ] **Support team updated**: What to watch for, how to answer questions
- [ ] **Sales team updated** (if user-facing): New features to promote
- [ ] **Marketing team updated** (if user-facing): Release materials ready

---

## Support Team Readiness

### Support Documentation

- [ ] **Support docs updated**: Internal knowledge base current
- [ ] **Canned responses ready**: FAQs prepared
- [ ] **Known issues documented**: Workarounds available
- [ ] **Escalation procedures updated**: When to escalate to engineering

### Support Metrics

- [ ] **Ticket volume normal**: Not spiking unexpectedly
- [ ] **Ticket topics normal**: No new recurring issues
- [ ] **Response times acceptable**: Support team keeping up
- [ ] **Resolution times normal**: Issues being resolved

---

## Cleanup Tasks

### Code Cleanup

- [ ] **Old versions removed**: Unused containers/artifacts deleted
- [ ] **Feature flags cleaned** (if done): Removed temporary flags
- [ ] **Debug logging reduced** (if added): Verbose logging disabled
- [ ] **Comments cleaned up**: Removed "TODO: remove after deploy"

### Infrastructure Cleanup

- [ ] **Blue environment stopped** (if blue-green): Old environment deallocated
- [ ] **Old caches invalidated**: Stale CDN content purged
- [ ] **DNS TTL restored** (if changed): TTL set back to normal
- [ ] **Rate limits restored** (if changed): Back to production values

---

## Compliance & Audit

### Audit Trail

- [ ] **Deployment logged**: Who, what, when, why recorded
- [ ] **Approvals captured**: Sign-offs documented
- [ ] **Configuration changes logged**: Tracked in audit system
- [ ] **Access logs reviewed**: No unauthorized access

### Compliance

- [ ] **Change management ticket updated**: JIRA/ServiceNow closed
- [ ] **Release register updated**: Official release log maintained
- [ ] **Compliance notifications sent** (if required): Audit team informed

---

## Risk Assessment (Ongoing)

### Monitoring for Issues

- [ ] **Monitoring dashboards reviewed**: Regular check-ins scheduled
- [ ] **Alert noise assessed**: Alerts tuned appropriately
- [ ] **On-call load balanced**: Engineers not overwhelmed
- [ ] **Incident rate normal**: No increase in incidents

### Early Warning Signs (Watch For)

- ⚠️ **Gradual performance degradation**: Slow creep in response times
- ⚠️ **Subtle error rate increase**: Small but sustained error increase
- ⚠️ **Memory usage climbing**: Potential memory leak
- ⚠️ **Queue depth growing**: Background jobs falling behind
- ⚠️ **User complaints emerging**: Support tickets increasing
- ⚠️ **Business metrics dipping**: Conversions slowly declining

---

## Phased Rollout Verification (If Using Feature Flags or Canary)

### Phase Progression

- [ ] **Phase 1 complete (5% rollout)**: No issues detected
- [ ] **Phase 1 metrics reviewed**: Error rates, performance acceptable
- [ ] **Phase 2 complete (25% rollout)**: Stable expansion
- [ ] **Phase 2 metrics reviewed**: Continued healthy metrics
- [ ] **Phase 3 complete (50% rollout)**: Half of users served
- [ ] **Phase 3 metrics reviewed**: Sustained stability
- [ ] **Phase 4 complete (100% rollout)**: Full deployment
- [ ] **Phase 4 metrics reviewed**: All users successfully migrated

### Cohort Analysis

- [ ] **Cohort comparison**: 100% vs previous cohorts
- [ ] **No cohort-specific issues**: All user groups performing similarly
- [ ] **Feature adoption by cohort**: Usage patterns as expected

---

## 24-Hour Health Report

### Executive Summary

- [ ] **Overall health**: Green/Yellow/Red status
- [ ] **Key metrics summary**: Error rates, performance, business KPIs
- [ ] **Issues encountered**: List any problems
- [ ] **User feedback summary**: Support tickets, sentiment
- [ ] **Recommendation**: Continue monitoring, rollback, or hotfix

### Report Distribution

- [ ] **Engineering leadership**: VP Eng, CTO, etc.
- [ ] **Product leadership**: CPO, PM, etc.
- [ ] **Business stakeholders**: CEO, COO, etc. (for major releases)
- [ ] **Support team**: Customer-facing teams

---

## Long-Term Monitoring (T+24 to T+48 Hours)

### Sustained Health

- [ ] **48-hour metrics stable**: No degradation over 2 days
- [ ] **User feedback positive**: Overall sentiment good
- [ ] **Business impact positive**: KPIs improving or stable
- [ ] **Team confident**: No lingering concerns

### Transition to Normal Operations

- [ ] **Intensive monitoring ended**: Return to standard monitoring
- [ ] **On-call handoff complete**: Normal on-call rotation resumed
- [ ] **Deployment channel archived**: Close temporary channels
- [ ] **Retrospective scheduled**: Set date within 1 week

---

## Retrospective Preparation

### Data to Collect

- [ ] **Deployment timeline**: How long each phase took
- [ ] **Issues log**: What went wrong
- [ ] **Wins log**: What went well
- [ ] **Metrics snapshot**: Pre/post comparison
- [ ] **Team feedback**: Survey or async feedback
- [ ] **User feedback**: Support ticket themes

---

## Final Sign-Off

- [ ] **Release stable after 24 hours**: Monitoring shows healthy system
- [ ] **No critical issues**: All blockers resolved
- [ ] **Documentation complete**: All records updated
- [ ] **Communication complete**: All stakeholders informed
- [ ] **Normal operations resumed**: Back to standard procedures

---

**Release Manager Sign-Off**: _________________

**24-Hour Health Status**: ☐ Green (Healthy)  ☐ Yellow (Concerns)  ☐ Red (Issues)

**Date/Time of Final Verification**: _________________

**Recommendation**: ☐ Continue Monitoring  ☐ Schedule Hotfix  ☐ Initiate Rollback

**Notes**:
