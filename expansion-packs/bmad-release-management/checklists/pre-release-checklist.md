# Pre-Release Quality Gates Checklist

Use this checklist to validate that a release meets quality standards before deployment to production. These are the gates that must pass for a go/no-go decision.

## Code Quality Gates

### Testing

- [ ] **All tests passing**: Unit, integration, and end-to-end tests all green
- [ ] **Test coverage meets threshold**: Minimum 80% code coverage (or team-defined threshold)
- [ ] **No flaky tests**: All tests are reliable and deterministic
- [ ] **Performance tests passed**: Load tests meet defined SLAs
- [ ] **Regression tests completed**: No existing functionality broken
- [ ] **Edge cases tested**: Error handling, boundary conditions validated
- [ ] **Cross-browser testing** (if web app): Works in all supported browsers
- [ ] **Mobile responsiveness tested** (if applicable): iOS and Android validated

### Code Review

- [ ] **All PRs reviewed**: No unreviewed code in release
- [ ] **All review comments addressed**: No open conversations or requested changes
- [ ] **Architecture review completed** (for significant changes): Technical design approved
- [ ] **No "TODO" or "FIXME" comments**: All placeholders resolved
- [ ] **Code formatting consistent**: Linter passing

### Static Analysis

- [ ] **Linting passed**: No linting errors or warnings
- [ ] **Code smells addressed**: SonarQube or similar tool reviewed
- [ ] **Complexity metrics acceptable**: No overly complex functions
- [ ] **Dead code removed**: No unused imports, functions, or files

## Security Gates

### Vulnerability Scanning

- [ ] **SAST scan clean**: Static application security testing passed
- [ ] **DAST scan clean** (if applicable): Dynamic application security testing passed
- [ ] **No critical vulnerabilities**: Zero critical or high-severity issues
- [ ] **Medium vulnerabilities documented**: Known issues with mitigation plans
- [ ] **Dependency scanning clean**: No known CVEs in dependencies
- [ ] **Container scanning passed** (if using containers): Base images secure
- [ ] **Secrets scanning**: No API keys, passwords, or tokens in code

### Security Best Practices

- [ ] **Authentication tested**: Login/logout flows validated
- [ ] **Authorization verified**: Permissions and role checks working
- [ ] **Input validation implemented**: SQL injection, XSS protections in place
- [ ] **HTTPS enforced** (if web app): No mixed content warnings
- [ ] **Security headers configured**: CSP, HSTS, X-Frame-Options, etc.
- [ ] **API rate limiting implemented**: Protection against abuse
- [ ] **Sensitive data encrypted**: PII encrypted at rest and in transit

## Performance Gates

### Performance Metrics

- [ ] **Response times acceptable**: p50, p95, p99 within SLA
- [ ] **Throughput meets target**: Requests per second as expected
- [ ] **Resource utilization healthy**: CPU, memory, disk within limits
- [ ] **Database queries optimized**: No N+1 queries, indexes used
- [ ] **Bundle size optimized** (if web app): JavaScript/CSS bundles within budget
- [ ] **Images optimized**: Compressed and properly sized
- [ ] **Caching configured**: Redis, CDN, browser caching working

### Load Testing

- [ ] **Load tests passed**: System handles expected traffic
- [ ] **Stress tests passed**: System degrades gracefully under extreme load
- [ ] **Spike tests passed**: Handles sudden traffic increases
- [ ] **Soak tests passed**: No memory leaks over extended periods
- [ ] **Concurrency tests passed**: Race conditions handled

## Documentation Gates

### Technical Documentation

- [ ] **API documentation updated**: Endpoints, parameters, responses documented
- [ ] **README updated**: Installation, configuration instructions current
- [ ] **Architecture diagrams updated**: System design reflects current state
- [ ] **Database schema documented**: ERD or schema docs updated
- [ ] **Configuration documented**: Environment variables, settings explained
- [ ] **Deployment docs updated**: Deployment procedures reflect changes

### User-Facing Documentation

- [ ] **User guide updated**: New features documented
- [ ] **Help center updated**: FAQs, tutorials current
- [ ] **Release notes drafted**: User-friendly change summary prepared
- [ ] **Changelog updated**: Technical changelog from conventional commits
- [ ] **Migration guide created** (if breaking changes): Step-by-step upgrade instructions
- [ ] **Known issues documented**: Workarounds provided

## Database & Infrastructure

### Database

- [ ] **Migrations tested in staging**: Database changes validated
- [ ] **Migrations are reversible**: Rollback procedures work
- [ ] **Migrations are backward compatible**: Old app version works during migration
- [ ] **Data migration scripts tested**: Data transformation validated
- [ ] **Backup created**: Recent backup available for restore
- [ ] **Database performance tested**: Indexes created, query plans reviewed

### Infrastructure

- [ ] **Infrastructure as code updated**: Terraform, CloudFormation, etc. current
- [ ] **Capacity planning reviewed**: Sufficient resources allocated
- [ ] **Monitoring configured**: Metrics, logs, alerts set up
- [ ] **Alerting thresholds defined**: When to notify on-call
- [ ] **Health checks implemented**: Liveness and readiness probes working
- [ ] **Scaling policies configured**: Auto-scaling rules defined

## Release Preparation

### Release Artifacts

- [ ] **Build successful**: CI/CD pipeline green
- [ ] **Artifacts created**: Docker images, binaries, packages built
- [ ] **Artifacts tagged**: Version numbers applied
- [ ] **Artifacts signed** (if applicable): Cryptographic signatures for verification
- [ ] **Artifacts uploaded**: To artifact repository or registry

### Planning & Communication

- [ ] **Release plan complete**: All sections filled in release plan document
- [ ] **Scope finalized**: What's in and what's deferred
- [ ] **Version number determined**: SemVer or CalVer version selected
- [ ] **Target date confirmed**: Release window scheduled
- [ ] **Rollback plan documented**: How to revert if issues arise
- [ ] **Feature flags configured**: Flags set to appropriate values
- [ ] **Deployment runbook ready**: Step-by-step deployment guide

### Stakeholder Alignment

- [ ] **Product owner approval**: PO signed off on release
- [ ] **QA sign-off**: QA team approved
- [ ] **Security team approval** (if required): Security review complete
- [ ] **Stakeholders notified**: Release plan shared
- [ ] **Support team briefed**: Customer support prepared for inquiries
- [ ] **Marketing aligned** (if user-facing): Communications coordinated

## Environment Readiness

### Staging Environment

- [ ] **Staging deployment successful**: Release deployed and tested in staging
- [ ] **Staging smoke tests passed**: Key flows validated
- [ ] **Staging matches production**: Environment parity confirmed
- [ ] **No staging-specific issues**: No environment-specific bugs

### Production Environment

- [ ] **Maintenance window scheduled** (if needed): Downtime window communicated
- [ ] **On-call team scheduled**: Engineers available during/after deployment
- [ ] **Runbook accessible**: Deployment steps available to team
- [ ] **Credentials validated**: All necessary access confirmed
- [ ] **Rate limits increased** (if needed): API quotas adjusted for migration traffic

## Compliance & Legal

### Compliance

- [ ] **GDPR compliance verified** (if applicable): Data privacy requirements met
- [ ] **SOC 2 requirements met** (if applicable): Audit trail, access controls
- [ ] **HIPAA compliance verified** (if applicable): Healthcare data protections
- [ ] **Accessibility standards met** (if applicable): WCAG 2.1 AA compliance
- [ ] **License compliance checked**: All dependencies have compatible licenses

### Legal

- [ ] **Terms of service updated** (if needed): Legal documents current
- [ ] **Privacy policy updated** (if needed): Data handling disclosed
- [ ] **Legal review completed** (if required): For significant changes

## Team Readiness

### Deployment Team

- [ ] **Deployment team identified**: Who will execute deployment
- [ ] **Team availability confirmed**: All required people available
- [ ] **Roles assigned**: Clear ownership for each step
- [ ] **Communication channels active**: Slack, Teams, Discord ready
- [ ] **Escalation path defined**: Who to contact if issues arise

### Support Team

- [ ] **Support documentation updated**: Internal knowledge base current
- [ ] **Support team trained**: Aware of new features and changes
- [ ] **Canned responses prepared**: For common expected questions
- [ ] **Escalation procedures updated**: Technical support contacts

## Risk Assessment

### Risk Evaluation

- [ ] **Risk assessment completed**: High, medium, low risks identified
- [ ] **Mitigation strategies defined**: Plan for each significant risk
- [ ] **Blast radius understood**: Scope of impact if deployment fails
- [ ] **Critical dependencies identified**: External services, APIs, vendors
- [ ] **Failure scenarios documented**: What could go wrong and how to respond

### Rollback Readiness

- [ ] **Rollback criteria defined**: When to trigger rollback
- [ ] **Rollback tested in staging**: Rollback procedure validated
- [ ] **Rollback automation working**: Scripts or tools tested
- [ ] **Rollback owner assigned**: Who makes rollback decision

## Release Type-Specific Gates

### For Major Releases (Breaking Changes)

- [ ] **Beta/RC testing completed**: Pre-release versions tested by users
- [ ] **Migration path tested**: Upgrade process validated end-to-end
- [ ] **Backward compatibility period defined**: How long old version supported
- [ ] **Deprecation notices sent**: Users warned well in advance (2-4 weeks)
- [ ] **Partner/integration notifications sent**: Third-party integrations informed

### For Hotfixes

- [ ] **Root cause identified**: Problem fully understood
- [ ] **Fix verified**: Issue resolution confirmed
- [ ] **Minimal scope confirmed**: Only critical fix included
- [ ] **Fast-track approval obtained**: Leadership aware and approved
- [ ] **Post-incident plan ready**: Post-mortem scheduled

### For Database-Heavy Releases

- [ ] **Data validation scripts ready**: Verify data integrity post-migration
- [ ] **Rollback window realistic**: Time to rollback if needed
- [ ] **Database replication verified**: Replicas in sync
- [ ] **Connection pooling tuned**: Sufficient connections available

## Final Go/No-Go Decision

### Go Criteria (All Must Be True)

- [ ] **All critical gates passed**: No critical issues remain
- [ ] **Medium issues accepted**: Team consciously accepts known issues
- [ ] **Stakeholders aligned**: All required approvals obtained
- [ ] **Team confident**: Deployment team feels prepared
- [ ] **Rollback plan ready**: Team can revert quickly if needed

### No-Go Criteria (Any Triggers No-Go)

- ⚠️ **Critical test failures**: Core functionality broken
- ⚠️ **Critical security vulnerabilities**: Unpatched high-severity issues
- ⚠️ **Missing stakeholder approval**: Required sign-off not obtained
- ⚠️ **Incomplete documentation**: Users won't know how to use new features
- ⚠️ **Team not ready**: Key people unavailable or unprepared
- ⚠️ **Production environment issues**: Infra problems detected
- ⚠️ **No rollback plan**: Can't safely revert if needed

---

## Gate Exceptions

Sometimes gates must be bypassed (e.g., critical hotfix during outage). If skipping gates:

1. **Document the exception**: Why gate was skipped
2. **Get explicit approval**: From VP Engineering, CTO, or equivalent
3. **Create remediation tasks**: Schedule time to address skipped gates
4. **Add extra monitoring**: Compensate for reduced confidence
5. **Plan immediate follow-up**: Hotfix the hotfix if needed

---

**Remember**: These gates exist to protect users, the business, and the team. Skipping them should be rare and deliberate, never casual.

## Quality Gate Sign-Off

- [ ] **QA Lead Sign-Off**: _________________ Date: _______
- [ ] **Security Lead Sign-Off**: _________________ Date: _______
- [ ] **Engineering Lead Sign-Off**: _________________ Date: _______
- [ ] **Product Owner Sign-Off**: _________________ Date: _______

**Final Decision**: ☐ GO  ☐ NO-GO  ☐ GO WITH CONDITIONS

**Conditions (if applicable)**:
