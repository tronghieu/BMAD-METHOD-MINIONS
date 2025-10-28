# Deployment Patterns Guide

## Overview

Deployment patterns are proven strategies for releasing software to production with minimal risk and maximum confidence. The right pattern depends on your application architecture, team capabilities, and risk tolerance.

## Core Deployment Goals

1. **Zero or Minimal Downtime**: Users shouldn't notice the deployment
2. **Fast Rollback**: Ability to quickly revert if issues arise
3. **Progressive Exposure**: Test with small audiences before full rollout
4. **Observability**: Monitor health throughout deployment
5. **Repeatability**: Consistent process every time

---

## Deployment Patterns

### 1. Recreate (All-at-Once) Deployment

**How it Works**:
1. Stop all instances of old version
2. Deploy new version
3. Start all instances of new version

**Visual Flow**:
```
Old: [V1] [V1] [V1]
     ↓    ↓    ↓
Down: [ ] [ ] [ ]  (downtime period)
     ↓    ↓    ↓
New: [V2] [V2] [V2]
```

**Characteristics**:
- ⏱️ Downtime: Yes (minutes)
- 💰 Cost: Low (no extra resources)
- 🔧 Complexity: Simple
- ⚡ Rollback: Slow (requires redeployment)

**When to Use**:
- ✅ Development/staging environments
- ✅ Internal tools with flexible downtime windows
- ✅ Applications where downtime is acceptable
- ✅ Database migrations that require exclusive access

**When NOT to Use**:
- ❌ Production systems requiring high availability
- ❌ Customer-facing applications
- ❌ Applications with SLA commitments

**Example Use Case**:
Internal admin dashboard that's only used during business hours. Deploy during evening maintenance window.

---

### 2. Rolling Deployment

**How it Works**:
1. Update instances incrementally
2. Wait for health check before proceeding to next
3. Continue until all instances updated

**Visual Flow**:
```
Start:  [V1] [V1] [V1] [V1]
Step 1: [V2] [V1] [V1] [V1]  (update 1st)
Step 2: [V2] [V2] [V1] [V1]  (update 2nd)
Step 3: [V2] [V2] [V2] [V1]  (update 3rd)
End:    [V2] [V2] [V2] [V2]  (all updated)
```

**Characteristics**:
- ⏱️ Downtime: No
- 💰 Cost: Low (no extra resources)
- 🔧 Complexity: Moderate
- ⚡ Rollback: Moderate (roll forward or back)

**Configuration Options**:
- **Batch size**: How many instances to update at once
- **Wait time**: Pause between batches for monitoring
- **Health check**: Validation before proceeding

**When to Use**:
- ✅ Backward-compatible changes
- ✅ Stateless applications
- ✅ Applications with multiple instances
- ✅ When you want to minimize resource usage

**When NOT to Use**:
- ❌ Breaking changes requiring all-or-nothing deployment
- ❌ Database schema changes affecting compatibility
- ❌ When you need instant rollback capability

**Example Use Case**:
E-commerce website with 10 application servers. Roll update across 2 servers at a time, waiting 10 minutes between batches.

---

### 3. Blue-Green Deployment

**How it Works**:
1. Maintain two identical environments (Blue = current, Green = new)
2. Deploy new version to Green environment
3. Test Green thoroughly
4. Switch traffic from Blue to Green instantly
5. Keep Blue as rollback option

**Visual Flow**:
```
Before:
  Blue (V1): [Active] ← 100% traffic
  Green:     [Idle]

During:
  Blue (V1): [Active] ← 100% traffic
  Green (V2): [Testing] (deploy & verify)

After Switch:
  Blue (V1): [Standby] (ready for rollback)
  Green (V2): [Active] ← 100% traffic
```

**Characteristics**:
- ⏱️ Downtime: None (instant switch)
- 💰 Cost: High (2x resources)
- 🔧 Complexity: Moderate
- ⚡ Rollback: Instant (switch back)

**When to Use**:
- ✅ Production deployments requiring instant rollback
- ✅ When you can afford duplicate infrastructure
- ✅ Releases with higher risk
- ✅ Applications requiring extensive pre-production validation

**When NOT to Use**:
- ❌ Stateful applications (database sync challenges)
- ❌ Tight budget constraints
- ❌ Very large infrastructure (2x cost prohibitive)

**Example Use Case**:
Banking application where rollback must be instant and downtime is unacceptable. Maintain complete duplicate environment.

**Implementation Considerations**:
- **Database handling**: Use read replicas or shared database
- **Session management**: Use sticky sessions or external session store
- **Switching mechanism**: Load balancer, DNS, or API gateway

---

### 4. Canary Deployment

**How it Works**:
1. Deploy new version to small subset of instances
2. Route small percentage of traffic to new version
3. Monitor metrics closely
4. Gradually increase traffic if healthy
5. Roll out to 100% or rollback if issues detected

**Visual Flow**:
```
Phase 1: 5% traffic
  V1: [▓▓▓▓▓▓▓▓▓▓] ← 95%
  V2: [▓]         ← 5%

Phase 2: 25% traffic
  V1: [▓▓▓▓▓▓]    ← 75%
  V2: [▓▓▓]       ← 25%

Phase 3: 50% traffic
  V1: [▓▓▓▓▓]     ← 50%
  V2: [▓▓▓▓▓]     ← 50%

Phase 4: 100% traffic
  V1: []          ← 0%
  V2: [▓▓▓▓▓▓▓▓▓▓] ← 100%
```

**Characteristics**:
- ⏱️ Downtime: None
- 💰 Cost: Low to moderate
- 🔧 Complexity: High
- ⚡ Rollback: Fast (reduce traffic to 0%)

**Typical Phases**:
1. Internal users (5%)
2. Early adopters (25%)
3. Half of users (50%)
4. All users (100%)

**When to Use**:
- ✅ High-risk releases
- ✅ Large user bases (meaningful sample sizes)
- ✅ When you have strong monitoring
- ✅ Applications where gradual rollout is safe

**When NOT to Use**:
- ❌ Small user bases (insufficient sample size)
- ❌ Changes that must be atomic (all users at once)
- ❌ Poor monitoring infrastructure

**Example Use Case**:
Social media platform rolling out new algorithm. Start with 5% of users, monitor engagement metrics, gradually expand if positive.

**Key Metrics to Monitor**:
- Error rates (4xx, 5xx responses)
- Response times (p50, p95, p99)
- Business metrics (conversion, engagement)
- Resource utilization (CPU, memory)

---

### 5. Feature Flags (Feature Toggles)

**How it Works**:
1. Deploy code to production with features disabled
2. Enable features for specific users/groups via configuration
3. Monitor and gradually expand enabled users
4. Remove flag once feature is stable

**Visual Flow**:
```
Deploy:
  Code: [V2 with FeatureX disabled]
  All Users: See V1 behavior

Phase 1:
  Internal team: See FeatureX
  Other users: See V1 behavior

Phase 2:
  25% users: See FeatureX
  75% users: See V1 behavior

Cleanup:
  All users: See FeatureX
  Remove flag code
```

**Characteristics**:
- ⏱️ Downtime: None
- 💰 Cost: Low (infrastructure), Moderate (development overhead)
- 🔧 Complexity: Moderate to high
- ⚡ Rollback: Instant (toggle off)

**Types of Feature Flags**:

**Release Flags** (temporary)
- Control rollout of new features
- Remove after full deployment
- Lifespan: Days to weeks

**Operational Flags** (long-lived)
- Kill switches for resource-intensive features
- Premium features
- Lifespan: Months to years

**Experimental Flags** (temporary)
- A/B testing
- Hypothesis validation
- Lifespan: Duration of experiment

**When to Use**:
- ✅ Decoupling deployment from release
- ✅ A/B testing
- ✅ Gradual feature rollout
- ✅ Kill switch for expensive operations

**When NOT to Use**:
- ❌ Every single change (too much overhead)
- ❌ Without flag cleanup process
- ❌ As substitute for good branching strategy

**Example Use Case**:
E-commerce platform adding new recommendation engine. Deploy code in off state, enable for 10% of users, measure conversion lift, expand or revert.

**Feature Flag Tools**:
- LaunchDarkly (SaaS)
- Split.io (SaaS)
- Unleash (open source)
- Flagsmith (open source)
- Roll your own (simple database flag)

---

## Database Migration Strategies

Database changes are often the riskiest part of deployments. Use these strategies to manage them safely.

### 1. Expand-Contract Pattern

**Three-Phase Approach**:

**Phase 1: Expand** (non-breaking)
- Add new columns/tables alongside old ones
- Deploy application that writes to both old and new
- Backfill data from old to new

**Phase 2: Migrate** (transition)
- Update application to read from new schema
- Continue writing to both
- Validate data consistency

**Phase 3: Contract** (cleanup)
- Update application to only use new schema
- Remove old columns/tables
- Remove migration code

**Example**: Renaming a column

```sql
-- Phase 1: Expand (Release N)
ALTER TABLE users ADD COLUMN email_address VARCHAR(255);
UPDATE users SET email_address = email WHERE email_address IS NULL;

-- Application writes to both: user.email and user.email_address

-- Phase 2: Migrate (Release N+1)
-- Application reads from email_address, writes to both

-- Phase 3: Contract (Release N+2)
ALTER TABLE users DROP COLUMN email;
-- Application only uses email_address
```

### 2. Backward Compatible Migrations

**Rules**:
- Never rename columns in place (use expand-contract)
- Never remove columns immediately (deprecate first)
- Never change column types directly (add new, migrate, remove old)
- Always make columns nullable initially
- Use default values to avoid breaking reads

**Safe Operations** (can do immediately):
- ✅ Add new table
- ✅ Add new column (nullable or with default)
- ✅ Add new index
- ✅ Insert new data

**Unsafe Operations** (require expand-contract):
- ❌ Rename column
- ❌ Remove column
- ❌ Change column type
- ❌ Add NOT NULL constraint to existing column
- ❌ Delete table

### 3. Migration Rollback Plans

**Rollback Strategy Checklist**:
- [ ] Can migration be rolled back automatically?
- [ ] Does rollback require manual intervention?
- [ ] Is data loss acceptable if rolled back?
- [ ] Have you tested rollback in staging?

**Types of Migrations**:

**Reversible** (can rollback cleanly):
```sql
-- UP
ALTER TABLE users ADD COLUMN phone VARCHAR(20);

-- DOWN
ALTER TABLE users DROP COLUMN phone;
```

**One-Way** (cannot rollback without data loss):
```sql
-- UP
ALTER TABLE users DROP COLUMN legacy_field;

-- Cannot rollback without data loss!
```

**Irreversible but Safe** (can rollback app, keep schema):
```sql
-- UP
ALTER TABLE orders ADD COLUMN status_v2 VARCHAR(50);
-- App uses status_v2, but status remains

-- ROLLBACK: App switches back to status column
```

---

## Health Checks and Readiness

### Health Check Types

**Liveness Probe**
- "Is the application running?"
- Answers: Yes (200 OK) or No (500 Error)
- If fails: Restart container/instance

**Readiness Probe**
- "Is the application ready to serve traffic?"
- Checks dependencies (database, cache, external APIs)
- If fails: Remove from load balancer

**Startup Probe**
- "Has the application finished starting?"
- Gives time for slow-starting applications
- Prevents premature liveness failures

### Health Check Implementation

**Endpoint Example**: `GET /health`

```json
{
  "status": "healthy",
  "version": "2.1.0",
  "checks": {
    "database": "ok",
    "cache": "ok",
    "external_api": "ok"
  },
  "uptime": 3600,
  "timestamp": "2024-01-15T10:30:00Z"
}
```

**Best Practices**:
- Lightweight (< 100ms response time)
- Check critical dependencies
- Return 200 for healthy, 500+ for unhealthy
- Include version information
- Don't check external services in liveness probe

---

## Rollback Strategies

### Automated Rollback Triggers

Automatically rollback when:
- Error rate exceeds threshold (e.g., >1% 5xx responses)
- Response time degrades significantly (e.g., p95 > 2x baseline)
- Health checks fail on >20% of instances
- Critical business metrics drop (e.g., conversion rate drops >10%)

### Manual Rollback Decision Tree

```
Is production impact critical? (outage, data loss, security)
├─ YES → Immediate rollback
└─ NO → Is issue fixable with hotfix?
    ├─ YES → Deploy hotfix forward
    └─ NO → Does issue affect <10% of users?
        ├─ YES → Use feature flag to disable
        └─ NO → Rollback
```

### Rollback Methods by Deployment Pattern

| Pattern | Rollback Method | Rollback Time |
|---------|----------------|---------------|
| **Recreate** | Redeploy old version | 5-15 minutes |
| **Rolling** | Roll back in reverse | 10-30 minutes |
| **Blue-Green** | Switch traffic back | Seconds |
| **Canary** | Reduce traffic to 0% | Seconds |
| **Feature Flag** | Toggle off | Seconds |

---

## Deployment Checklist

### Pre-Deployment
- [ ] All tests passing (unit, integration, e2e)
- [ ] Code review completed
- [ ] Security scans clean
- [ ] Database migrations tested in staging
- [ ] Rollback plan documented
- [ ] Monitoring alerts configured
- [ ] On-call team notified
- [ ] Communication sent to stakeholders

### During Deployment
- [ ] Create backup (database, config)
- [ ] Run database migrations
- [ ] Deploy application code
- [ ] Execute smoke tests
- [ ] Verify health checks
- [ ] Monitor error rates
- [ ] Check key business metrics

### Post-Deployment
- [ ] Confirm all instances healthy
- [ ] Verify user-facing functionality
- [ ] Monitor for 30 minutes minimum
- [ ] Update documentation
- [ ] Send completion notification
- [ ] Document any issues encountered

---

## Choosing the Right Pattern

### Decision Matrix

| Requirement | Best Pattern |
|-------------|--------------|
| **Zero downtime required** | Blue-Green, Canary, Feature Flags |
| **Instant rollback needed** | Blue-Green, Feature Flags |
| **Limited budget/resources** | Rolling, Recreate |
| **High risk release** | Canary, Blue-Green |
| **A/B testing** | Feature Flags |
| **Database schema changes** | Rolling + Expand-Contract |
| **Breaking changes** | Blue-Green or Feature Flags |
| **Gradual rollout preferred** | Canary, Feature Flags |

### Hybrid Approaches

**Canary + Feature Flags**
- Deploy code to canary with feature flagged off
- Enable feature for canary users
- Monitor and expand both deployment and flag

**Blue-Green + Feature Flags**
- Deploy to green with features flagged off
- Switch to green
- Gradually enable features via flags

**Rolling + Expand-Contract Migrations**
- Deploy database migration in phase 1 (expand)
- Roll out application reading new schema
- Later deploy phase 3 (contract) to cleanup

---

## Tools and Technologies

### Container Orchestration
- **Kubernetes**: Built-in support for rolling, canary via service mesh
- **Docker Swarm**: Rolling updates supported
- **ECS/Fargate**: Blue-green and rolling deployments

### Service Mesh
- **Istio**: Traffic splitting for canary
- **Linkerd**: Progressive delivery
- **Consul Connect**: Traffic management

### CI/CD Tools
- **GitHub Actions**: Workflow automation
- **GitLab CI/CD**: Built-in deployment strategies
- **Jenkins**: Customizable pipelines
- **ArgoCD**: GitOps for Kubernetes

### Feature Flag Services
- **LaunchDarkly**: Enterprise feature management
- **Split.io**: Feature flags + experimentation
- **Unleash**: Open source feature toggles

---

## Best Practices

1. **Always have a rollback plan** - Hope for the best, plan for the worst
2. **Monitor continuously** - You can't fix what you can't see
3. **Deploy during low-traffic periods** when possible
4. **Use automation** to reduce human error
5. **Test in production-like environments** first
6. **Keep deployments small** - Easier to debug and rollback
7. **Document everything** - Future you will thank present you
8. **Practice rollbacks** - Don't wait for an emergency to test them
9. **Communicate clearly** - Keep stakeholders informed
10. **Learn from each deployment** - Retrospectives drive improvement

## Anti-Patterns

❌ **Deploying on Fridays** (weekend incident response)
❌ **Skipping staging** ("test in production")
❌ **No monitoring plan** (flying blind)
❌ **Manual, undocumented processes** (tribal knowledge)
❌ **Large batch deployments** (high risk)
❌ **No rollback plan** (hope-driven development)
❌ **Ignoring health checks** (partial outages)
❌ **Cowboy deployments** (no coordination)
