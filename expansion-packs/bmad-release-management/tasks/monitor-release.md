# Task: Monitor Release

**Release Management Phase**: Post-Deployment Monitoring
**Duration**: 24-48 hours (with check-ins)
**Agent**: Release Manager
**Difficulty**: Medium

## Purpose

Continuously monitor the release after deployment to ensure it remains stable and healthy. This task catches issues early and provides data for retrospective analysis.

## Prerequisites

Before starting this task, ensure you have:

- [ ] **Deployment completed successfully**: Release is live in production
- [ ] **Monitoring dashboards accessible**: All metrics visible
- [ ] **Baseline metrics documented**: Pre-release performance data
- [ ] **Alert thresholds configured**: Notifications set up
- [ ] **On-call team available**: Engineers ready to respond
- [ ] **Post-deployment checklist**: `checklists/post-deployment-checklist.md`

## Step-by-Step Process

### Phase 1: Intensive Monitoring (First 4 Hours)

#### 1.1 Hour 1: Critical Observation Period

**Every 15 minutes, check**:

**Error Rates**:
```
Time        5xx Errors   4xx Errors   Exceptions
15:15       0.08%        2.1%         3/min     ✅
15:30       0.12%        2.3%         5/min     ✅
15:45       0.09%        2.0%         4/min     ✅
16:00       0.11%        2.2%         4/min     ✅
```

**Performance Metrics**:
```
Time        p50     p95     p99     Throughput
15:15       120ms   420ms   890ms   125 req/s  ✅
15:30       118ms   425ms   895ms   128 req/s  ✅
15:45       122ms   430ms   900ms   124 req/s  ✅
16:00       119ms   422ms   885ms   127 req/s  ✅
```

**Red Flags** (immediate attention):
- Error rate >2% sustained
- Response time >2x baseline
- Throughput dropped >30%
- Memory continuously climbing
- New error types appearing

**Yellow Flags** (watch closely):
- Error rate 1-2%
- Response time 1.5x baseline
- Throughput down 15-30%
- Gradual memory increase

#### 1.2 Review Error Logs

Check for new error patterns:

```bash
# View recent errors
kubectl logs -l app=myapp --since=1h | grep ERROR

# Count error types
kubectl logs -l app=myapp --since=1h | grep ERROR | sort | uniq -c

# Look for stack traces
kubectl logs -l app=myapp --since=1h | grep -A 10 "Exception"
```

**Look for**:
- Errors that didn't exist before deployment
- High frequency errors (>10/min)
- Database connection errors
- External API timeouts
- Authentication/authorization failures

#### 1.3 Check Business Metrics

Verify business operations normal:

```
Metric                  Baseline    Current    Status
User sign-ups/hour      50          48         ✅ (-4%)
Conversion rate         3.2%        3.3%       ✅ (+3%)
Transaction success     99.5%       99.4%      ✅ (-0.1%)
API calls/minute        850         880        ✅ (+4%)
```

**Red Flags**:
- Conversion rate drops >20%
- Transaction success <95%
- Sign-ups dropped significantly

#### 1.4 Monitor Infrastructure

Check system health:

```
Resource          Baseline    Current    Status
CPU usage         45%         48%        ✅
Memory usage      60%         65%        ✅
Disk I/O          20MB/s      22MB/s     ✅
Network traffic   15MB/s      16MB/s     ✅
```

**Red Flags**:
- CPU >80% sustained
- Memory >85% or continuously climbing
- Disk I/O maxed out
- Network saturation

#### 1.5 Post Hour 1 Update

Send status update to team:

```
✅ v2.1.0 - Hour 1 Status

Error Rate: 0.10% (baseline: 0.08%) ✅
Response Time p95: 425ms (baseline: 450ms) ✅
Business Metrics: All normal ✅
Issues: None

Continuing monitoring...
```

**Repeat for Hours 2, 3, and 4** with 30-minute check intervals.

---

### Phase 2: Extended Monitoring (4-24 Hours)

#### 2.1 Four-Hour Check-ins

**At +4h, +8h, +12h, +16h, +20h, +24h**:

**Cumulative Metrics Review**:
```
Last 4 Hours Summary:
- Total 5xx errors: 45 (baseline: 38) - +18% ⚠️
- Average response time p95: 440ms (baseline: 450ms) ✅
- Total transactions: 15,240 (baseline: 15,000) ✅
- Error breakdown:
  * TimeoutException: 32
  * NullPointerException: 8
  * DatabaseException: 5
```

**Trend Analysis**:
- Are errors increasing, decreasing, or stable?
- Is performance degrading over time?
- Are business metrics trending correctly?

**Example Check-in Report**:
```
✅ v2.1.0 - 4 Hour Status

Overall Health: Green

Error Rate: 0.11% (slightly elevated but acceptable)
Performance: Stable, within baseline
Business Metrics: +3% improvement in conversions
New Issues: None

Notable Observations:
- TimeoutException frequency increased slightly (investigating)
- Memory usage stable at 65%
- No user-reported issues

Next check-in: +8 hours
```

#### 2.2 Review Support Tickets

Check for user-reported issues:

**Support Ticket Analysis**:
```
Period: First 8 hours post-deployment

Total tickets: 23 (baseline: 20/8hrs)
New issues: 2
Known issues: 21

New Issue #1: "Login slower than usual" - 3 reports
Severity: Low
Action: Monitoring, no immediate action needed

New Issue #2: "Export to CSV broken" - 1 report
Severity: Medium
Action: Investigating
```

**Red Flags**:
- Ticket volume >2x normal
- Multiple reports of same new issue
- Critical functionality broken

#### 2.3 Monitor User Sentiment

Check social media, community forums:
- Twitter mentions
- Community Discord/Slack
- App store reviews (if mobile)
- Reddit posts

**Look for**:
- Complaints about new bugs
- Performance complaints
- Praise for new features (good sign!)

#### 2.4 Track Feature Adoption (if using feature flags)

For newly released features:

```
Feature: OAuth Authentication
Rollout: 25% of users

Adoption Rate: 18% of eligible users tried it
Success Rate: 99.2% successful authentications
User Feedback: Mostly positive (3 issues reported)
```

**Decision Point**: Continue rollout or hold?

---

### Phase 3: 24-Hour Health Assessment

#### 3.1 Compile 24-Hour Metrics

Create comprehensive report:

**Error Metrics (24 hours)**:
```
Metric                  Baseline    Actual     Change
5xx Error Rate          0.08%       0.11%      +38%    ⚠️
4xx Error Rate          2.1%        2.0%       -5%     ✅
Exception Count         480/day     520/day    +8%     ⚠️
Total Incidents         0           0          0       ✅
```

**Performance Metrics (24 hours)**:
```
Metric                  Baseline    Actual     Change
Response Time p50       120ms       118ms      -2%     ✅
Response Time p95       450ms       440ms      -2%     ✅
Response Time p99       900ms       920ms      +2%     ✅
Throughput             120 req/s    127 req/s  +6%     ✅
```

**Business Metrics (24 hours)**:
```
Metric                  Baseline    Actual     Change
Daily Sign-ups          1,200       1,215      +1%     ✅
Conversion Rate         3.2%        3.3%       +3%     ✅
Transaction Success     99.5%       99.4%      -0.1%   ✅
Revenue                 $50,000     $51,500    +3%     ✅
```

**Infrastructure Metrics (24 hours)**:
```
Metric                  Baseline    Actual     Status
Max CPU                 65%         68%        ✅
Max Memory              75%         78%        ✅
Avg Memory              60%         65%        ✅
Disk Usage              45%         46%        ✅
```

#### 3.2 Analyze Error Patterns

Group and prioritize errors:

**Top Errors (24 hours)**:
```
Error Type              Count    % of Total   Severity
TimeoutException        385      74%          Medium
NullPointerException    92       18%          Low
DatabaseException       43       8%           Medium

Total: 520 errors (baseline: 480)
```

For each error type:
- Is it new or pre-existing?
- Is frequency acceptable?
- Needs immediate fix or can wait?

#### 3.3 User Feedback Summary

Compile user reports:

**Support Tickets (24 hours)**:
```
Total: 48 tickets (baseline: 50)
New issues: 3
Known issues: 45

New Issue Summary:
1. Login performance - 8 reports (Low severity)
2. Export CSV - 2 reports (Medium severity)
3. Dark mode display bug - 1 report (Low severity)
```

**Sentiment Analysis**:
- Overall sentiment: Positive
- Feature reception: Good (OAuth praised)
- No critical complaints

#### 3.4 Make 24-Hour Decision

**Health Status**: Green / Yellow / Red

**Green** (All good):
- All metrics within acceptable range
- No critical issues
- User feedback positive
- Recommendation: Continue normal monitoring

**Yellow** (Minor concerns):
- Some metrics elevated but stable
- Minor issues with workarounds
- Mostly positive feedback
- Recommendation: Continue monitoring, create fix plan

**Red** (Significant issues):
- Critical metrics degraded
- Multiple serious issues
- Negative user impact
- Recommendation: Hotfix or rollback

#### 3.5 Send 24-Hour Report

**Report Template**:
```
📊 v2.1.0 - 24 Hour Health Report

Overall Status: GREEN ✅

Summary:
v2.1.0 has been stable for 24 hours. Minor error rate increase
(+38%) is under investigation but within acceptable limits.
Performance improved slightly. Business metrics show positive trend.

Metrics:
✅ Error Rate: 0.11% (acceptable)
✅ Performance: Improved over baseline
✅ Business Metrics: +3% conversion improvement
⚠️ Elevated TimeoutException (investigating)

User Feedback:
- 48 support tickets (normal volume)
- 3 new minor issues identified
- Overall sentiment positive

Incidents: 0

Recommendation: Continue monitoring. No action needed.

Action Items:
1. Investigate TimeoutException increase
2. Fix CSV export issue in next patch
3. Monitor login performance

Next Update: 48-hour final assessment

Thank you team! 🎉
```

**Distribution**: Email to stakeholders, post in Slack

---

### Phase 4: 48-Hour Final Assessment

#### 4.1 Confirm Sustained Stability

Verify metrics stable over 48 hours:
- No degradation trends
- Error rates plateaued
- Performance stable
- Business metrics positive

#### 4.2 Compare to Previous Releases

**Historical Comparison**:
```
Release     First 48h Incidents    Error Rate    Performance
v2.1.0      0                      0.11%        Improved
v2.0.0      1                      0.15%        Stable
v1.9.0      2                      0.20%        Degraded
```

**Analysis**: v2.1.0 is cleanest release in last 3 versions

#### 4.3 Document Learnings

Capture observations for retrospective:
- What went well
- What could be improved
- Unexpected issues
- Monitoring gaps discovered

#### 4.4 Transition to Normal Operations

**Final Report**:
```
✅ v2.1.0 - 48 Hour Final Assessment

Release Status: STABLE

v2.1.0 has been successfully running in production for 48 hours
with no incidents and improved performance metrics.

48-Hour Summary:
- Total Uptime: 100%
- Incidents: 0
- Error Rate: 0.11% (acceptable, investigating cause)
- Performance: 2% improvement over baseline
- Business Impact: +3% conversion rate
- User Feedback: Positive

Conclusion: Release is healthy and stable.

Transitioning to normal monitoring operations.
Retrospective scheduled for [Date].

Thank you deployment team! 🚀
```

**Actions**:
- Return to standard on-call rotation
- Close intensive monitoring
- Archive deployment channel
- Schedule retrospective

---

## Expected Outputs

At the end of this task, you should have:

1. **Hourly Monitoring Logs**: First 4 hours detailed tracking
2. **24-Hour Health Report**: Comprehensive metrics analysis
3. **48-Hour Final Assessment**: Stability confirmation
4. **Issue Log**: All problems discovered
5. **User Feedback Summary**: Support tickets and sentiment
6. **Trend Analysis**: Performance over time
7. **Retrospective Prep**: Data for learning session
8. **Updated Release Plan**: Post-release monitoring section filled

## Common Challenges & Solutions

### Challenge: "Error rate elevated but unclear if serious"

**Solutions**:
- Compare to historical baselines
- Analyze error types (new vs known)
- Check if errors have user impact
- When in doubt, investigate thoroughly
- Create hotfix plan as precaution

### Challenge: "Metrics look good but users complaining"

**Solutions**:
- Metrics don't capture everything
- Listen to user feedback carefully
- Investigate specific complaints
- Check for edge cases or specific user segments
- Users are the ultimate quality measure

### Challenge: "One metric degraded, others fine"

**Solutions**:
- Assess overall health holistically
- Understand metric relationships
- Check if degradation is acceptable
- Monitor for trends (getting worse?)
- Plan fix if impact is significant

### Challenge: "Too many metrics to track"

**Solutions**:
- Focus on critical business metrics
- Use dashboards with pre-built views
- Set up automated alerts
- Have monitoring observer dedicated role
- Automate metric collection and reporting

## Success Indicators

You'll know this task was successful when:

✅ **No critical incidents**: Release remained stable
✅ **Metrics within range**: All KPIs acceptable
✅ **Issues caught early**: Problems identified quickly
✅ **User feedback positive**: Minimal complaints
✅ **Team confidence high**: Release validated
✅ **Data collected**: Rich dataset for retrospective
✅ **Smooth transition**: Normal operations resumed

## Related Resources

- **Post-Deployment Checklist**: `checklists/post-deployment-checklist.md` - Verification steps
- **Knowledge Base**: `data/release-management-kb.md` - Monitoring best practices
- **Release Plan**: `templates/release-plan.md` - Where to document monitoring results

## Next Tasks

After monitoring period:
→ **conduct-retrospective.md** - Learn from the release (2-3 days after deployment)
→ **rollback-release.md** - If critical issues discovered (hope not!)
