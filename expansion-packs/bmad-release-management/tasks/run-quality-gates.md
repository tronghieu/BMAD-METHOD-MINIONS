# Task: Run Quality Gates

**Release Management Phase**: Quality Validation
**Duration**: 30-90 minutes
**Agent**: Quality Gatekeeper
**Difficulty**: Medium-High

## Purpose

Systematically validate that the release meets all quality standards before deployment to production. This task prevents shipping broken, insecure, or poorly performing releases by enforcing objective quality criteria.

## Prerequisites

Before starting this task, ensure you have:

- [ ] **Release scope finalized**: Know what's being released
- [ ] **Access to CI/CD pipeline**: Can view test results
- [ ] **Access to security scanning tools**: SAST, DAST, dependency scanning
- [ ] **Access to monitoring**: Performance metrics, error rates
- [ ] **Pre-release checklist available**: `checklists/pre-release-checklist.md`
- [ ] **Staging environment available**: Production-like environment for testing
- [ ] **Time buffer**: Run this 24-48 hours before deployment for remediation time

## Step-by-Step Process

### Phase 1: Test Coverage Validation (10-15 minutes)

#### 1.1 Check Test Execution

Verify all tests are running and passing:

```bash
# Run full test suite
npm test              # or yarn test, pytest, etc.
npm run test:integration
npm run test:e2e

# Check test results in CI
# GitHub Actions, GitLab CI, Jenkins, etc.
```

**Verify**:
- [ ] Unit tests: All passing
- [ ] Integration tests: All passing
- [ ] End-to-end tests: All passing
- [ ] No skipped or ignored tests (without good reason)

**If failures exist**:
- Document each failure
- Assess criticality (test bug vs real bug)
- Fix real bugs or defer feature if not fixable quickly

#### 1.2 Check Test Coverage

Review code coverage metrics:

```bash
# Generate coverage report
npm run test:coverage

# Check coverage thresholds
# Typical targets: 80%+ total, 70%+ for new code
```

**Acceptance Criteria**:
- Total coverage: ≥ 80% (or team-defined threshold)
- New code coverage: ≥ 70%
- Critical paths: 100% (authentication, payments, data integrity)

**If coverage is low**:
- Identify uncovered critical code
- Add tests for high-risk areas
- Accept lower coverage with documented reason
- Create follow-up tasks for coverage improvement

#### 1.3 Review Test Quality

Not just quantity—check test quality:
- [ ] Tests actually assert meaningful behavior
- [ ] Tests cover happy path AND error cases
- [ ] Integration tests cover key workflows
- [ ] E2E tests cover critical user journeys
- [ ] No placeholder tests ("TODO: write test")

**Document**: Coverage percentage, any gaps, remediation plan

### Phase 2: Security Scanning (15-20 minutes)

#### 2.1 Run Static Application Security Testing (SAST)

Scan source code for vulnerabilities:

```bash
# Example tools
npm audit                    # Node.js dependencies
pip-audit                    # Python dependencies
bundle audit                 # Ruby dependencies
snyk test                    # Multi-language
semgrep --config=auto .     # Code patterns
```

**Review Results**:
- **Critical vulnerabilities**: MUST fix before release (zero tolerance)
- **High vulnerabilities**: Assess risk, fix or document accept risk
- **Medium vulnerabilities**: Review, plan fix for next release
- **Low vulnerabilities**: Note for future improvement

**Acceptance Criteria**:
- Zero critical vulnerabilities
- Zero high vulnerabilities in production code paths
- All medium/low vulnerabilities reviewed and accepted

#### 2.2 Run Dynamic Application Security Testing (DAST)

Scan running application for vulnerabilities:

```bash
# Example tools
# OWASP ZAP, Burp Suite, Acunetix
# Usually run in CI against staging environment
```

**Check for**:
- SQL injection vulnerabilities
- Cross-site scripting (XSS)
- Authentication bypasses
- Session management issues
- Insecure configurations

**Acceptance Criteria**:
- Zero critical findings
- Zero high findings
- Medium findings reviewed and mitigated or accepted

#### 2.3 Dependency Vulnerability Scan

Check third-party dependencies:

```bash
# Check for known CVEs
npm audit
snyk test --severity-threshold=high
```

**Review Dependencies**:
- [ ] No dependencies with critical CVEs
- [ ] No dependencies with high CVEs (or acceptable risk documented)
- [ ] Dependencies reasonably up-to-date
- [ ] No deprecated packages in critical paths

**If vulnerabilities found**:
- Update dependencies if patches available
- Find alternative package if no patch exists
- Document acceptance if no fix available (rare)

#### 2.4 Container Security (If Using Containers)

Scan Docker images:

```bash
# Scan container images
docker scan myapp:latest
trivy image myapp:latest
snyk container test myapp:latest
```

**Check**:
- [ ] Base image up-to-date and from trusted source
- [ ] No critical vulnerabilities in image layers
- [ ] Minimal image size (fewer attack vectors)

**Document**: All security scan results, vulnerabilities, remediation status

### Phase 3: Performance Validation (15-20 minutes)

#### 3.1 Run Performance Benchmarks

Execute performance tests:

```bash
# Example: Run load tests
artillery run load-test.yaml
k6 run performance-test.js
```

**Key Metrics**:
- Response time (p50): ______ms (Target: <200ms)
- Response time (p95): ______ms (Target: <500ms)
- Response time (p99): ______ms (Target: <1000ms)
- Throughput: ______ req/s (Target: >100 req/s)
- Error rate under load: ______% (Target: <1%)

**Acceptance Criteria**:
- All metrics within or better than baseline
- No degradation >10% from previous release
- No memory leaks detected
- CPU usage within acceptable limits

#### 3.2 Compare with Baseline

Compare current performance to previous release:

```
Metric              Baseline    Current    Change
Response Time p95   450ms       420ms      -7% ✅
Throughput          120 req/s   125 req/s  +4% ✅
Error Rate          0.1%        0.08%      -20% ✅
Memory Usage        450MB       480MB      +7% ⚠️
```

**Red Flags**:
- Response time increased >20%
- Throughput decreased >10%
- Error rate increased significantly
- Memory usage growing (potential leak)

#### 3.3 Check Database Performance

Review database query performance:

```sql
-- Check slow query log
-- Identify queries >1 second

-- Check for missing indexes
EXPLAIN SELECT ...

-- Review query execution plans
```

**Verify**:
- [ ] No new slow queries introduced
- [ ] All frequently-used queries indexed
- [ ] N+1 queries eliminated
- [ ] Connection pool size appropriate

**Document**: Performance metrics, any regressions, optimization notes

### Phase 4: Functional Validation (15-20 minutes)

#### 4.1 Deploy to Staging

Ensure staging environment mirrors production:

```bash
# Deploy to staging
# Verify deployment successful
# Smoke test critical paths
```

**Staging Environment Checklist**:
- [ ] Same infrastructure as production (containers, services, etc.)
- [ ] Same database version
- [ ] Production-like data volume
- [ ] External integrations configured (or mocked appropriately)

#### 4.2 Execute Smoke Tests

Test critical user journeys:

**Critical Path Tests**:
- [ ] User can sign up / register
- [ ] User can log in
- [ ] Core feature #1 works: _____________
- [ ] Core feature #2 works: _____________
- [ ] Core feature #3 works: _____________
- [ ] Payment processing works (if applicable)
- [ ] Data is persisted correctly

**Integration Tests**:
- [ ] External APIs responding
- [ ] Email delivery working
- [ ] File uploads/downloads working
- [ ] Search functionality working

#### 4.3 Check for Regressions

Test areas that might be affected by changes:
- Run full regression test suite
- Manually test related features
- Check for UI/UX issues

**Document**: All test results, any issues found

### Phase 5: Documentation Review (5-10 minutes)

#### 5.1 Verify Documentation Completeness

Check that documentation is updated:

**User-Facing Documentation**:
- [ ] New features documented
- [ ] Changed behavior explained
- [ ] Screenshots/GIFs updated
- [ ] Help center articles updated

**Technical Documentation**:
- [ ] API documentation current (OpenAPI/Swagger)
- [ ] Breaking changes documented
- [ ] Migration guides complete
- [ ] Configuration changes documented

**Internal Documentation**:
- [ ] Deployment runbook updated
- [ ] Architecture diagrams current
- [ ] Troubleshooting guides updated

#### 5.2 Review Release Notes

Verify release notes are ready:
- [ ] Changelog complete and accurate
- [ ] Release notes user-friendly
- [ ] Breaking changes prominently displayed
- [ ] Upgrade instructions clear
- [ ] Known issues documented

### Phase 6: Code Review Status (5 minutes)

#### 6.1 Verify All PRs Reviewed

Check that all code was reviewed:

```bash
# List merged PRs since last release
gh pr list --state merged --base main --search "merged:>{{last_release_date}}"
```

**Verify**:
- [ ] All PRs have approvals (2+ reviewers ideal)
- [ ] No self-merged PRs (except emergencies)
- [ ] All review comments addressed
- [ ] No unresolved conversations

#### 6.2 Check for Hot Fixes

Review any emergency fixes merged:
- Were they properly reviewed post-merge?
- Do they have tests?
- Are they documented?

### Phase 7: Compliance & Audit (5-10 minutes)

#### 7.1 Check Regulatory Compliance

If applicable to your industry:

**GDPR Compliance** (if handling EU user data):
- [ ] Data processing documented
- [ ] User privacy controls working
- [ ] Data deletion functionality
- [ ] Privacy policy updated

**HIPAA Compliance** (if healthcare):
- [ ] PHI encryption at rest and in transit
- [ ] Audit logging enabled
- [ ] Access controls verified

**SOC 2 Compliance** (if enterprise SaaS):
- [ ] Change management process followed
- [ ] Access logs maintained
- [ ] Security controls documented

#### 7.2 License Compliance

Verify dependency licenses compatible:

```bash
# Check licenses
npx license-checker --summary
```

**Verify**:
- [ ] No GPL licenses (unless your project is GPL)
- [ ] All licenses documented
- [ ] License compatibility reviewed

### Phase 8: Make Go/No-Go Recommendation (5 minutes)

#### 8.1 Assess Overall Quality

Review all gate results:

**Critical Gates** (Must Pass):
- ✅/❌ All tests passing
- ✅/❌ Zero critical security vulnerabilities
- ✅/❌ Performance within acceptable limits
- ✅/❌ Staging deployment successful
- ✅/❌ Critical functionality works

**Important Gates** (Should Pass):
- ✅/❌ Test coverage meets threshold
- ✅/❌ No high security vulnerabilities
- ✅/❌ Documentation complete
- ✅/❌ All PRs reviewed

#### 8.2 Calculate Quality Score

Tally results:
- Critical gates passed: ___/5
- Important gates passed: ___/4
- Known issues: ___
- Accepted risks: ___

#### 8.3 Make Recommendation

**GO - Recommend proceeding with release**:
- All critical gates passed
- Most important gates passed
- Any failures have acceptable workarounds
- Team confident in quality

**NO-GO - Recommend blocking release**:
- Any critical gate failed
- Multiple important gates failed
- Unacceptable risks identified
- Team lacks confidence

**CONDITIONAL GO - Recommend with conditions**:
- Critical gates passed
- Some important gates failed with acceptable reasons
- Conditions documented and agreed
- Increased monitoring planned

#### 8.4 Document Decision

Create quality gate report:

```markdown
## Quality Gate Report - v2.1.0

**Overall Recommendation**: GO / NO-GO / CONDITIONAL GO

**Critical Gates**: 5/5 Passed ✅
**Important Gates**: 3/4 Passed ⚠️

**Details**:
- Testing: ✅ All tests passing, 85% coverage
- Security: ✅ Zero critical/high vulnerabilities
- Performance: ✅ All metrics within SLA
- Staging: ✅ Deployment successful, smoke tests passed
- Documentation: ⚠️ API docs 90% complete (acceptable)

**Known Issues**:
1. Minor UI issue on mobile Safari - workaround documented

**Accepted Risks**:
1. Medium security vulnerability in dev dependency (non-production)

**Decision**: GO
**Decision Maker**: {{QA Lead Name}}
**Date**: {{Date}}

**Sign-Offs Required**:
- [ ] QA Lead
- [ ] Security Lead
- [ ] Engineering Lead
- [ ] Product Owner
```

### Phase 9: Get Stakeholder Sign-Off (5 minutes)

#### 9.1 Present Results

Share quality gate report with:
- Release Manager
- Engineering Lead
- Product Owner
- Security Lead (if applicable)

#### 9.2 Address Concerns

If stakeholders have concerns:
- Present data and evidence
- Explain accepted risks
- Propose additional monitoring
- Adjust recommendation if needed

#### 9.3 Obtain Approvals

Get formal sign-offs:
- [ ] QA Lead: _____________ Date: _______
- [ ] Security Lead: _____________ Date: _______
- [ ] Engineering Lead: _____________ Date: _______
- [ ] Product Owner: _____________ Date: _______

#### 9.4 Update Release Plan

Add quality assessment to release plan document:
- Quality gate results
- Go/no-go decision
- Known issues
- Accepted risks
- Sign-offs

## Expected Outputs

At the end of this task, you should have:

1. **Quality Gate Report**: Comprehensive assessment of release quality
2. **Test Results**: All test execution results documented
3. **Security Scan Results**: All vulnerability scans completed and reviewed
4. **Performance Metrics**: Benchmark results vs baseline
5. **Staging Validation**: Smoke test results from staging
6. **Documentation Status**: Completeness check
7. **Go/No-Go Decision**: Clear recommendation with rationale
8. **Stakeholder Sign-Offs**: Formal approvals obtained
9. **Updated Release Plan**: Quality section filled in

## Common Challenges & Solutions

### Challenge: "Tests are failing but we need to ship"

**Solutions**:
- Assess if failing tests are critical
- Fix bugs if real issues
- Fix or remove flaky tests
- Never ship with failing critical tests
- Defer features with failing tests

### Challenge: "Security scan found vulnerabilities with no fixes available"

**Solutions**:
- Check if vulnerability is exploitable in your context
- Look for alternative packages
- Implement mitigating controls
- Document accepted risk with leadership approval
- Plan fix for next release

### Challenge: "Performance degraded but unsure why"

**Solutions**:
- Profile application to find bottleneck
- Compare code changes that might impact performance
- Check for N+1 queries or missing indexes
- Consider deferring performance-impacting features
- Add performance monitoring to production

### Challenge: "Not enough time to fix all issues"

**Solutions**:
- Triage: Fix critical, defer non-critical
- Extend deployment date if needed
- Reduce scope (defer problematic features)
- Remember: Shipping broken software costs more than delays

### Challenge: "Pressure to skip quality gates"

**Solutions**:
- Show historical data: quality issues cost time/money
- Propose reduced scope instead
- Escalate to engineering leadership
- Stand firm: quality gates exist for good reasons

## Success Indicators

You'll know this task was successful when:

✅ **Comprehensive assessment**: All quality dimensions checked
✅ **Objective evaluation**: Based on data, not opinions
✅ **Clear decision**: Go/no-go recommendation with solid rationale
✅ **Stakeholder alignment**: Everyone understands quality status
✅ **Documentation complete**: Results captured for retrospective
✅ **Confidence level high**: Team feels good about release quality
✅ **Risks understood**: Any issues documented and accepted
✅ **Sign-offs obtained**: Formal approvals in place

## Related Resources

- **Checklist**: `checklists/pre-release-checklist.md` - Comprehensive quality gates
- **Knowledge Base**: `data/release-management-kb.md` - Quality gate philosophy
- **Release Plan**: `templates/release-plan.md` - Where to document results

## Next Tasks

After completing quality gates:
→ **plan-deployment.md** - Create detailed deployment plan (if go decision)
→ **analyze-scope.md** - Reduce scope and re-run gates (if no-go due to issues)
