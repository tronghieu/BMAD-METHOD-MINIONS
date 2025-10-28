# Task: Create Release Plan

**Release Management Phase**: Planning
**Duration**: 60-120 minutes
**Agent**: Release Manager
**Difficulty**: Medium

## Purpose

Co-create a comprehensive release plan document with the user that serves as the single source of truth for the entire release lifecycle. This document guides the release from planning through deployment, monitoring, and retrospective.

## Prerequisites

Before starting this task, ensure you have:

- [ ] **Release goals understood**: Why are we releasing now?
- [ ] **Work completed or near completion**: Features/fixes ready or nearly ready
- [ ] **Stakeholders identified**: Who needs to be involved?
- [ ] **Access to git history**: Can review commits since last release
- [ ] **Access to issue tracker**: Can review completed issues/PRs
- [ ] **Previous release plan** (if exists): Learn from past releases
- [ ] **Target date identified**: When should this ship?

## Step-by-Step Process

### Phase 1: Release Overview (15-20 minutes)

#### 1.1 Determine Version Number

Ask user about changes to determine appropriate version:

**Questions to ask**:
- "Are there any breaking changes or BC breaks?"
- "What new features are included?"
- "Are there only bug fixes?"
- "Is this a critical hotfix?"

**Apply versioning strategy** (refer to `data/versioning-strategies.md`):

**If using Semantic Versioning (SemVer)**:
- Breaking changes → **MAJOR** version bump (e.g., 1.x.x → 2.0.0)
- New features (backward compatible) → **MINOR** bump (e.g., 1.2.x → 1.3.0)
- Bug fixes only → **PATCH** bump (e.g., 1.2.3 → 1.2.4)
- Critical hotfix → **PATCH** bump with expedited process

**If using Calendar Versioning (CalVer)**:
- Use current date: YYYY.MM.DD or YYYY.MM.MICRO

Document the version and rationale in the release plan.

#### 1.2 Define Release Type

Classify the release:
- **Major Release**: Breaking changes, significant features, long planning cycle
- **Minor Release**: New features, standard planning cycle
- **Patch Release**: Bug fixes, streamlined process
- **Hotfix**: Critical production issue, emergency process

This determines which workflow to follow.

#### 1.3 Establish Release Goals

Work with user to define:
- **Primary goal**: What's the main reason for this release?
- **Secondary goals**: What else do we hope to achieve?
- **Success criteria**: How will we know this release succeeded?

Examples:
- "Ship new payment integration to expand to EU market"
- "Fix critical security vulnerability affecting 20% of users"
- "Deliver Q1 roadmap commitments to enterprise customers"

#### 1.4 Identify Stakeholders

List all people who need to be involved:
- **Release Manager**: Who's leading this release?
- **Product Owner**: Who owns the product vision?
- **Engineering Lead**: Who's technically responsible?
- **QA Lead**: Who validates quality?
- **DevOps Lead**: Who manages deployment?
- **Communication Lead**: Who handles announcements?

#### 1.5 Set Target Date

Determine deployment window:
- **Target release date**: When should this ship?
- **Deployment window**: What time of day? (avoid Fridays, peak hours)
- **Flexibility**: Is this date firm or flexible?

Document any constraints (customer commitments, conference demos, etc.)

### Phase 2: Scope Analysis (20-30 minutes)

Use the **Scope Analyzer** agent for detailed analysis, or guide user through manually:

#### 2.1 Review Completed Work

**Check git history**:
```bash
git log v{{last_version}}..HEAD --oneline
git log v{{last_version}}..HEAD --pretty=format:"%h %s" | head -20
```

**Review closed issues/PRs**:
- GitHub: Filter by milestone or closed date range
- Jira: Sprint or release version filter
- GitLab: Milestone filter

#### 2.2 Categorize Changes

Group work into categories:
- **Features**: New functionality
- **Bug Fixes**: Problem resolutions
- **Breaking Changes**: Incompatible changes
- **Performance Improvements**: Speed/efficiency gains
- **Security Fixes**: Vulnerability patches
- **Documentation**: Doc updates only
- **Dependencies**: Library updates

#### 2.3 Assess Readiness

For each significant item, ask:
- Is it fully complete?
- Has it been tested?
- Is documentation updated?
- Are there known issues?

Mark items as:
- ✅ **Include**: Ready to ship
- ⏸️ **Defer**: Not ready, move to next release
- ⚠️ **Needs review**: Uncertain, discuss with team

#### 2.4 Identify Dependencies

Document any dependencies:
- **Internal**: Other features or fixes this depends on
- **External**: Third-party services, APIs
- **Coordination**: Other teams that must deploy simultaneously

#### 2.5 Document Scope

Fill in the **Scope** section of release-plan.md:
- List all included items with issue numbers
- List deferred items with reasons
- Note any dependencies or risks

### Phase 3: Generate Changelog (15-20 minutes)

Refer to `data/changelog-conventions.md` for format guidance.

#### 3.1 Parse Git History

If using Conventional Commits:
```bash
git log v{{last_version}}..HEAD --pretty=format:"%s" | grep "^feat:"
git log v{{last_version}}..HEAD --pretty=format:"%s" | grep "^fix:"
git log v{{last_version}}..HEAD --pretty=format:"%s" | grep "^BREAKING:"
```

#### 3.2 Categorize Changes

Organize commits into categories:
- **Breaking Changes** (⚠️ Always list first!)
- **Added** (new features)
- **Changed** (modifications to existing features)
- **Deprecated** (marked for future removal)
- **Removed** (deleted features)
- **Fixed** (bug fixes)
- **Security** (🔒 security patches)
- **Performance** (speed improvements)

#### 3.3 Write Clear Entries

For each change:
- Start with action verb (Added, Fixed, Changed, Removed)
- Be specific and clear
- Link to issue/PR number
- Focus on WHAT changed, not HOW

**Good examples**:
- "Added dark mode support to user settings (#234)"
- "Fixed crash when uploading files over 100MB (#456)"
- "Changed API response format from XML to JSON (#567)"

**Bad examples**:
- "Various bug fixes"
- "Updated code"
- "Improvements"

#### 3.4 Highlight Breaking Changes

For each breaking change:
- Explain what changed
- Describe the impact
- Provide migration instructions (brief here, detailed in Release Notes)

Example:
```
### Breaking Changes ⚠️

- **Changed authentication flow** - JWT tokens now expire after 1 hour instead of 24 hours.
  Clients must implement token refresh. Migration guide: [link] (#789)
```

#### 3.5 Review and Edit

- Remove noise (typo fixes, merge commits, etc.)
- Combine related commits
- Rewrite for clarity
- Ensure professional tone

Fill in the **Changelog** section of release-plan.md.

### Phase 4: Write Release Notes (15-20 minutes)

Transform technical changelog into user-friendly release notes.

#### 4.1 Highlight Top 3-5 Features

Choose the most impactful changes:
- What will users be most excited about?
- What solves major pain points?
- What's visually impressive?

For each highlight:
- Write user-friendly title
- Explain the benefit (not just the feature)
- Include screenshot, GIF, or demo link if possible

**Example transformation**:
- **Technical**: "Added Redis caching layer for user queries"
- **User-facing**: "⚡ Faster search results - We've turbocharged search to return results 5x faster!"

#### 4.2 List Improvements and Fixes

Summarize other changes:
- Group minor improvements
- Highlight important bug fixes
- Keep language simple and benefit-focused

#### 4.3 Document Breaking Changes (Critical!)

For user-facing breaking changes:
1. **What Changed**: Plain English explanation
2. **Who Is Affected**: Be specific about impact
3. **Action Required**: Step-by-step migration instructions
4. **Code Examples**: Before/after code snippets
5. **Migration Deadline**: If applicable

**Use warning emojis** (⚠️) and make this section highly visible.

#### 4.4 Write Upgrade Instructions

Provide clear upgrade steps:
- For end users (if applicable)
- For developers/API consumers
- For database migrations
- For configuration changes

Include actual commands they can copy-paste:
```bash
npm install myapp@2.0.0
npm run db:migrate
```

#### 4.5 Document Known Issues

Be transparent about known problems:
- List any known bugs or limitations
- Provide workarounds if available
- Link to issue tracker for status

Fill in the **Release Notes** section of release-plan.md.

### Phase 5: Quality Assessment (10-15 minutes)

Run the **Quality Gatekeeper** agent or manually check pre-release checklist.

#### 5.1 Review Pre-Release Checklist

Reference `checklists/pre-release-checklist.md` and document status:

**Critical gates**:
- [ ] All tests passing
- [ ] No critical security vulnerabilities
- [ ] Performance benchmarks met
- [ ] Documentation complete
- [ ] All PRs reviewed and approved

Record actual metrics:
- Test coverage: X%
- Security scan results: 0 critical, 2 medium
- Performance: p95 = Xms (baseline: Yms)

#### 5.2 Make Go/No-Go Recommendation

Based on quality gate results:
- **GO**: All critical gates passed, ready to deploy
- **NO-GO**: Critical issues remain, not safe to deploy
- **GO WITH CONDITIONS**: Most gates passed, accept specific risks

Document:
- Decision and rationale
- Who made the decision
- Any accepted risks or known issues
- Required sign-offs

Get stakeholder sign-offs if needed.

### Phase 6: Deployment Planning (15-20 minutes)

Work with **Deployment Coordinator** agent or plan manually.

Refer to `data/deployment-patterns.md` for strategy options.

#### 6.1 Select Deployment Pattern

Choose strategy based on risk and requirements:
- **Blue-Green**: Instant rollback needed, can afford 2x resources
- **Canary**: High risk, want gradual rollout
- **Rolling**: Standard deployment, minimize resource usage
- **Feature Flags**: Decouple deployment from release
- **Recreate**: Low-risk internal tool, downtime acceptable

Document choice and rationale.

#### 6.2 Plan Database Migrations

If database changes included:
- List migration scripts
- Choose strategy (expand-contract if breaking)
- Estimate duration
- Plan rollback approach

Reference `data/deployment-patterns.md` for migration patterns.

#### 6.3 Define Rollback Procedures

Critical: Plan how to revert if issues arise:
- What triggers rollback?
- Who decides to rollback?
- What are the steps?
- How long does rollback take?
- What data loss risks exist?

Be specific and realistic.

#### 6.4 Create Deployment Steps

Outline phase-by-phase deployment:
1. Pre-deployment tasks
2. Database migration steps
3. Application deployment steps
4. Smoke testing
5. Monitoring period

Include verification steps after each phase.

Fill in the **Deployment Plan** section of release-plan.md.

### Phase 7: Communications Planning (10-15 minutes)

Work with **Communication Specialist** agent or plan manually.

#### 7.1 Plan Internal Communications

Define messages for internal stakeholders:
- **T-24 hours**: Deployment notice
- **T-0**: Deployment starting
- **T+2 hours**: Deployment complete
- **T+24 hours**: Status update

#### 7.2 Plan External Communications

For user-facing releases:
- **Release announcement**: Blog post, email, social media
- **In-app notification**: Alert users to new features
- **Status page**: Maintenance window notice

Draft key messages (don't need to be perfect yet).

#### 7.3 Prepare Support Team

Create support briefing:
- What's new summary
- Expected common questions with answers
- Escalation path for issues
- Canned responses for common inquiries

Fill in the **Communications Plan** section of release-plan.md.

### Phase 8: Monitoring Planning (5-10 minutes)

#### 8.1 Define Key Metrics

List metrics to track post-deployment:
- **Error rates**: 4xx, 5xx, exceptions
- **Performance**: Response times (p50, p95, p99)
- **Infrastructure**: CPU, memory, disk
- **Business**: Conversions, sign-ups, transactions

#### 8.2 Set Alert Thresholds

For each metric, define:
- **Baseline**: Normal value
- **Warning threshold**: Investigate
- **Critical threshold**: Consider rollback

Example:
- 5xx error rate: Baseline 0.1%, Warning >0.5%, Critical >2%

#### 8.3 Plan Monitoring Duration

Define monitoring intensity:
- **First 4 hours**: Intensive, hourly checks
- **4-24 hours**: Extended, every 4-6 hours
- **24+ hours**: Normal monitoring

Fill in the **Monitoring Plan** section of release-plan.md.

### Phase 9: Review and Finalize (5-10 minutes)

#### 9.1 Review Complete Document

Walk through entire release plan:
- Is anything missing?
- Are all stakeholders identified?
- Is scope clear?
- Is rollback plan realistic?
- Are communications planned?

#### 9.2 Save to docs/release/ Directory

Save the release plan as:
```
docs/release/v{{version}}-release-plan.md
```

Example: `docs/release/v2.1.0-release-plan.md`

#### 9.3 Share with Stakeholders

Distribute plan to:
- Engineering team
- Product team
- QA team
- Support team
- Leadership (for major releases)

Get feedback and iterate if needed.

#### 9.4 Schedule Follow-Up Sessions

Plan upcoming sessions:
- Pre-deployment checklist review (T-24 hours)
- Deployment execution (deployment day)
- Post-deployment monitoring (T+4 hours, T+24 hours)
- Retrospective (T+2-3 days)

## Expected Outputs

At the end of this task, you should have:

1. **Comprehensive Release Plan Document**: `docs/release/v{{version}}-release-plan.md`
2. **Clear Scope**: What's included, what's deferred
3. **Technical Changelog**: For developers
4. **User-Friendly Release Notes**: For customers
5. **Quality Assessment**: Go/no-go decision
6. **Deployment Strategy**: How we'll deploy safely
7. **Communications Plan**: Who we'll tell, when, and how
8. **Monitoring Plan**: What we'll watch post-deployment
9. **Stakeholder Alignment**: Everyone knows the plan

## Common Challenges & Solutions

### Challenge: "Scope keeps changing"

**Solutions**:
- Set scope freeze date (e.g., T-48 hours)
- Create process for scope change requests
- Defer non-critical items to next release
- Communicate: "This release is locked, next release planning open"

### Challenge: "Can't decide on version number"

**Solutions**:
- Review `data/versioning-strategies.md` together
- Check for breaking changes (if any, it's MAJOR)
- When in doubt, be conservative (bump MAJOR if uncertain)
- Consistency matters more than perfection

### Challenge: "Too many items to include"

**Solutions**:
- Focus on completed, tested items only
- Split into two releases if needed
- Use feature flags to deploy code but enable later
- Defer lower-priority items

### Challenge: "User-facing release notes too technical"

**Solutions**:
- Have non-technical person review
- Focus on benefits, not implementation
- Use analogies and simple language
- Include visuals (screenshots, GIFs)
- Read release notes from companies with great UX (Figma, Linear, Notion)

### Challenge: "No time for thorough planning"

**Solutions**:
- For hotfix: Use streamlined hotfix workflow
- For standard release: Planning time is investment, not cost
- Bad deploys cost more time than good planning
- Minimum: Scope, rollback plan, monitoring plan

### Challenge: "Stakeholders not responsive"

**Solutions**:
- Set decision deadlines: "Need sign-off by EOD or we defer"
- Make plan visible (share in Slack, email, wiki)
- Escalate to leadership if blocking release
- Document attempted outreach

## Success Indicators

You'll know this task was successful when:

✅ **Comprehensive plan exists**: All sections filled with useful detail
✅ **Scope is clear**: Everyone knows what's in/out
✅ **Changelog is accurate**: Reflects actual changes
✅ **Release notes are user-friendly**: Non-technical people understand
✅ **Quality assessed**: Go/no-go decision made
✅ **Deployment planned**: Clear steps and rollback plan
✅ **Communications drafted**: Key messages prepared
✅ **Monitoring defined**: Know what to watch
✅ **Stakeholders aligned**: No surprises, everyone informed
✅ **Confidence level high**: Team feels prepared

## Tips for Different Release Types

### Hotfix Release (Expedited)
- Skip or streamline: Scope analysis (only fix), lengthy release notes
- Focus on: Rollback plan, monitoring, communication
- Use `workflows/hotfix-release.yaml`

### Major Release (Extended)
- Extra attention to: Breaking changes, migration guides, communications
- Consider: Beta/RC releases, phased rollout
- Add: Extended monitoring period, more thorough testing
- Use `workflows/major-release.yaml`

### Minor/Patch Release (Standard)
- Follow full process above
- Standard monitoring and rollback planning
- Use `workflows/standard-release.yaml`

## Time Variants

**Quick Planning (30-45 min)**:
- Focus on: Scope, version, deployment strategy, rollback plan
- Minimal: Release notes (can refine later)
- Skip: Detailed communications planning (draft quickly)

**Standard Planning (60-90 min)**:
- Follow full process above

**Thorough Planning (2-3 hours)**:
- Deep scope analysis
- Detailed risk assessment
- Comprehensive communications plan
- Team review session

## Related Resources

- **Knowledge Base**: `data/release-management-kb.md` - Release management philosophy
- **Versioning**: `data/versioning-strategies.md` - SemVer, CalVer guidance
- **Changelog**: `data/changelog-conventions.md` - Changelog format standards
- **Deployment**: `data/deployment-patterns.md` - Deployment strategies
- **Template**: `templates/release-plan.md` - Release plan template
- **Quality Gates**: `checklists/pre-release-checklist.md` - Quality validation

## Next Tasks

After completing release planning:
→ **analyze-scope.md** - Detailed scope analysis (if not done during planning)
→ **run-quality-gates.md** - Validate release quality (T-24 hours before deployment)
→ **plan-deployment.md** - Detailed deployment planning (if needed)
→ **execute-deployment.md** - Execute the deployment (deployment day)
