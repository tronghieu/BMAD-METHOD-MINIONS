# Task: Analyze Release Scope

**Release Management Phase**: Planning
**Duration**: 30-60 minutes
**Agent**: Scope Analyzer
**Difficulty**: Medium

## Purpose

Systematically review all completed work since the last release to determine what should be included in the upcoming release. This task ensures nothing important is missed and helps identify items that should be deferred.

## Prerequisites

Before starting this task, ensure you have:

- [ ] **Access to git repository**: Can review commit history
- [ ] **Access to issue tracker**: GitHub Issues, Jira, Linear, etc.
- [ ] **Last release version identified**: Know where to start analysis from
- [ ] **Project knowledge**: Understand what's been worked on recently
- [ ] **Release goals defined**: Know what the release is trying to achieve
- [ ] **Stakeholder input available**: Can ask questions if needed

## Step-by-Step Process

### Phase 1: Gather Work Items (10-15 minutes)

#### 1.1 Review Git History

Start by examining all commits since the last release:

```bash
# List all commits since last release
git log v{{last_version}}..HEAD --oneline

# Show detailed commit messages
git log v{{last_version}}..HEAD --pretty=format:"%h %s%n%b"

# Filter by author (if needed)
git log v{{last_version}}..HEAD --author="{{name}}"

# Show files changed
git log v{{last_version}}..HEAD --name-status
```

**Look for**:
- Feature commits (feat:, feature:, add:)
- Bug fixes (fix:, bugfix:, resolve:)
- Breaking changes (BREAKING, BREAKING CHANGE)
- Performance improvements (perf:, optimize:)
- Security fixes (security:, sec:, CVE)

#### 1.2 Review Closed Issues/PRs

Check your issue tracker for completed work:

**GitHub**:
- Go to Issues → Closed
- Filter by: `closed:>{{last_release_date}}`
- Check milestones or project boards

**Jira**:
- Filter: `status = Done AND resolved >= {{last_release_date}}`
- Look at sprint completion
- Check release versions

**GitLab/BitBucket**:
- Check closed merge requests
- Review milestone completion

#### 1.3 Review Story Files (if using BMAD)

If project uses BMAD methodology:
- Check `.bmad/stories/done/` directory
- Review completed story files
- Identify features marked as complete

#### 1.4 Gather Team Input

Ask development team:
- "What major features were completed?"
- "Are there any bug fixes we should highlight?"
- "Did we make any breaking changes?"
- "What performance improvements were made?"

### Phase 2: Categorize Changes (10-15 minutes)

#### 2.1 Create Categories

Organize items into standard changelog categories:

**Breaking Changes** ⚠️
- API changes that break compatibility
- Removed features
- Changed behavior that affects users
- Database schema changes requiring migration

**Features (Added)**
- New functionality
- New endpoints/APIs
- New user-facing capabilities
- New configuration options

**Enhancements (Changed)**
- Improvements to existing features
- Modified behavior (backward compatible)
- Updated dependencies
- Refactoring with user impact

**Bug Fixes (Fixed)**
- Resolved defects
- Corrected calculations
- Fixed crashes or errors
- Performance bug fixes

**Security Fixes** 🔒
- Vulnerability patches
- Security improvements
- Dependency updates (security-related)

**Performance Improvements**
- Speed optimizations
- Resource usage reduction
- Database query optimization

**Documentation**
- User documentation updates
- API documentation
- Code comments (if significant)

**Infrastructure/Internal**
- Build system changes
- CI/CD improvements
- Development tools
- (Usually not included in release notes)

#### 2.2 Document Each Item

For each significant change, capture:
- **Title**: Brief description
- **Type**: Category (feature, fix, breaking, etc.)
- **Issue/PR Number**: Link to tracking
- **Impact**: Who is affected?
- **Status**: Fully complete? Needs testing? Documentation done?
- **Notes**: Any special considerations

Example:
```
Title: Add OAuth2 authentication support
Type: Feature
Issue: #234
Impact: All users (optional feature)
Status: Complete, tested, documented
Notes: Requires configuration setup
```

### Phase 3: Assess Readiness (10-15 minutes)

#### 3.1 Evaluate Each Item

For every change, ask:

**Is it complete?**
- ✅ Code merged
- ✅ Tests passing
- ✅ Code reviewed
- ✅ Documentation updated
- ❌ Missing any of above → Not ready

**Is it tested?**
- ✅ Unit tests added
- ✅ Integration tests passing
- ✅ Manual testing done
- ✅ QA approved
- ❌ Insufficient testing → Risky

**Is it documented?**
- ✅ User-facing changes documented
- ✅ API changes documented
- ✅ Migration guide created (if breaking)
- ❌ Documentation missing → Not ready

**Does it have known issues?**
- No known bugs → Safe to ship
- Minor cosmetic issues → Acceptable
- Functional bugs → Defer or fix first
- Critical bugs → Must fix or defer

#### 3.2 Assign Readiness Status

Mark each item:

**✅ INCLUDE - Ready to ship**
- Fully complete
- Tested and working
- Documented
- No significant issues

**⏸️ DEFER - Not ready**
- Incomplete implementation
- Failing tests
- Missing documentation
- Known critical bugs
- Too risky for this release

**⚠️ CONDITIONAL - Needs review**
- Mostly ready but concerns exist
- Needs additional testing
- Documentation incomplete
- Minor known issues
- Discuss with team

**🔍 INVESTIGATE - Need more info**
- Unclear if complete
- Unknown testing status
- Needs stakeholder decision

### Phase 4: Identify Dependencies (5-10 minutes)

#### 4.1 Map Dependencies

For each item, identify:

**Code Dependencies**
- "Feature A requires Feature B to work"
- "Can't ship Feature X without Infrastructure Y"

**Team Dependencies**
- "Backend change requires mobile team to update"
- "API change needs documentation team to update docs"

**External Dependencies**
- "Requires new AWS service to be provisioned"
- "Needs third-party API key"
- "Depends on partner deployment"

**Sequential Dependencies**
- "Must deploy A before B"
- "Database migration must run first"

#### 4.2 Create Dependency Graph

Visualize dependencies if complex:
```
Feature A ← depends on → Infrastructure Z
    ↓
Feature B
    ↓
Feature C
```

Identify critical path items that block others.

### Phase 5: Make Inclusion Recommendations (10-15 minutes)

#### 5.1 Apply Inclusion Criteria

Use these criteria to recommend inclusion:

**Must Include**:
- Security fixes (always ship)
- Critical bug fixes (user-impacting)
- Committed features (customer/roadmap promises)
- Complete and tested items
- Dependencies of included items

**Should Include**:
- Completed features aligned with release goals
- Important bug fixes
- Performance improvements
- Items with no significant risks

**Consider Deferring**:
- Incomplete features (missing tests, docs)
- High-risk changes (major refactoring)
- Items with known significant bugs
- Nice-to-haves not aligned with release goals
- Items blocking other deferred items

**Must Defer**:
- Code not merged or reviewed
- Failing tests
- No documentation for user-facing changes
- Critical known bugs
- Depends on deferred items

#### 5.2 Assess Scope Balance

Evaluate the overall scope:

**Too Large?**
- 20+ significant items
- Multiple high-risk changes
- Many breaking changes
- Long deployment time expected
- High complexity

**Recommendation**: Split into two releases or defer lower-priority items

**Too Small?**
- <5 items
- Only minor bug fixes
- Very low impact
- Not worth release overhead

**Recommendation**: Wait for more items or bundle with next release

**Appropriate?**
- 5-15 significant items
- Mix of features and fixes
- Manageable risk level
- Aligns with release goals
- Clear user value

**Recommendation**: Proceed with release

#### 5.3 Consider Release Type

Scope should match release type:

**Hotfix Release**:
- Include: Critical fix only
- Defer: Everything else
- Keep scope minimal

**Patch Release**:
- Include: Bug fixes, minor improvements
- Defer: New features (save for minor)
- Keep backward compatible

**Minor Release**:
- Include: New features, enhancements, bug fixes
- Defer: Breaking changes (save for major)
- Maintain compatibility

**Major Release**:
- Include: Breaking changes, major features, cleanup
- Can include: Everything ready
- Good time for big changes

### Phase 6: Document Recommendations (5-10 minutes)

#### 6.1 Create Inclusion List

List all items recommended for inclusion:
```
INCLUDE IN v2.1.0:

Features:
- [#234] OAuth2 authentication support
- [#245] Dark mode theme option
- [#256] Export data to CSV

Bug Fixes:
- [#312] Fix crash on large file upload
- [#334] Correct timezone handling

Performance:
- [#401] Optimize database queries (40% faster)
```

#### 6.2 Create Deferral List

List all items recommended to defer with reasons:
```
DEFER TO v2.2.0:

- [#267] Advanced search filters - Incomplete testing
- [#289] Real-time collaboration - Missing documentation
- [#301] Admin dashboard redesign - Too risky, needs more review
- [#345] GraphQL API - Depends on #289, deferred
```

#### 6.3 Flag Items Needing Discussion

List uncertain items:
```
NEEDS DISCUSSION:

- [#278] New pricing model - Complete, but go-to-market not ready.
  Should we deploy code with feature flag OFF?

- [#290] Experimental AI feature - Tested but unclear if ready for
  production. Product team decision needed.
```

#### 6.4 Update Release Plan

Add scope analysis to the release plan document:
- Update "What's Included in This Release" section
- Update "What's NOT Included (Deferred)" section
- Update "Dependencies" section
- Add any risk notes

### Phase 7: Review with Stakeholders (5-10 minutes)

#### 7.1 Present Recommendations

Share scope analysis with:
- **Release Manager**: Overall decision maker
- **Product Owner**: Business priorities
- **Engineering Lead**: Technical feasibility
- **QA Lead**: Testing concerns

#### 7.2 Discuss Uncertain Items

For items marked "NEEDS DISCUSSION":
- Present the tradeoffs
- Get stakeholder input
- Make final inclusion decision
- Document rationale

#### 7.3 Get Sign-Off

Obtain agreement on final scope:
- [ ] Release Manager approves scope
- [ ] Product Owner confirms priorities
- [ ] Engineering Lead confirms technical readiness
- [ ] QA Lead confirms testing coverage

## Expected Outputs

At the end of this task, you should have:

1. **Complete Work Inventory**: List of all changes since last release
2. **Categorized Changes**: Items grouped by type (features, fixes, etc.)
3. **Readiness Assessment**: Status of each item (ready, not ready, etc.)
4. **Dependency Map**: Relationships between items
5. **Inclusion Recommendations**: What to include/defer with rationale
6. **Risk Assessment**: Identified risks for included items
7. **Updated Release Plan**: Scope section filled in
8. **Stakeholder Approval**: Agreement on final scope

## Common Challenges & Solutions

### Challenge: "Can't find all completed work"

**Solutions**:
- Check multiple sources: git, issues, project board, team chat
- Ask team members directly in standup
- Review sprint retrospectives for completed items
- Check feature flag configurations for hidden features

### Challenge: "Too many items, can't include all"

**Solutions**:
- Prioritize by: Security > Critical Bugs > Committed Features > Nice-to-haves
- Split into two releases: v2.1.0 (now) and v2.2.0 (2 weeks)
- Use feature flags to deploy code but enable later
- Be ruthless: defer anything not fully ready

### Challenge: "Items have complex dependencies"

**Solutions**:
- Draw dependency graph visually
- Include all dependent items or none
- Break dependencies with feature flags
- Defer dependent clusters to next release

### Challenge: "Unclear if item is ready"

**Solutions**:
- Check with item owner directly
- Review PR/issue status
- Run the feature yourself
- Mark as "NEEDS INVESTIGATION" and follow up
- When in doubt, defer (safer)

### Challenge: "Stakeholders disagree on priority"

**Solutions**:
- Present data: risk, completeness, user impact
- Let Product Owner make final call on features
- Let Engineering Lead make final call on technical risk
- Escalate to Release Manager for tiebreaking
- Document decision rationale

### Challenge: "Pressure to include incomplete items"

**Solutions**:
- Show risks clearly: "No tests means unknown bugs"
- Propose alternatives: feature flag, next release
- Stand firm on quality gates
- Escalate if pressure continues
- Remember: Bad releases cost more than delays

## Success Indicators

You'll know this task was successful when:

✅ **Comprehensive inventory**: All significant work identified
✅ **Clear categorization**: Items properly grouped
✅ **Objective assessment**: Readiness evaluated based on criteria, not opinion
✅ **Dependencies mapped**: No surprise blockers
✅ **Reasonable scope**: Not too large, not too small
✅ **Stakeholder alignment**: Everyone agrees on scope
✅ **Clear rationale**: Deferrals explained and documented
✅ **Updated release plan**: Scope section complete and accurate

## Tips for Different Situations

### Large Codebase / High Velocity Team
- Use automated tools to parse git history
- Group minor fixes together
- Focus on user-facing changes
- Skip internal refactoring in release notes

### Small Team / Low Activity
- Include even small improvements
- Combine multiple bug fixes
- Consider waiting to bundle more changes

### First Release (v1.0.0)
- List all major features
- Group by user benefit, not technical category
- Highlight what makes product valuable
- Less focus on "what's new" (everything is new)

### Hotfix Release
- Include ONLY the critical fix
- Explicitly list what's NOT included
- Defer everything else
- Keep scope minimal for fast deployment

## Related Resources

- **Knowledge Base**: `data/release-management-kb.md` - Scope management best practices
- **Changelog Guide**: `data/changelog-conventions.md` - How to categorize changes
- **Release Plan Template**: `templates/release-plan.md` - Where to document scope

## Next Tasks

After completing scope analysis:
→ **create-release-plan.md** - Use scope to finalize release plan (if not done)
→ **run-quality-gates.md** - Validate included items meet quality standards
