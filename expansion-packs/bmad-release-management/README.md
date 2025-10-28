# BMAD Release Management Expansion Pack

> **Comprehensive AI-powered release management framework for Agile software teams**

Transform your software release process from stressful chaos to predictable excellence with AI-powered release management agents that guide you through every phase—from planning to deployment to retrospectives.

---

## 📋 Table of Contents

- [Overview](#overview)
- [When to Use This Pack](#when-to-use-this-pack)
- [Quick Start](#quick-start)
- [Meet Your Team](#meet-your-team)
- [Workflows](#workflows)
- [What's Included](#whats-included)
- [Example Usage](#example-usage)
- [Best Practices](#best-practices)
- [Installation](#installation)

---

## Overview

The **BMAD Release Management** expansion pack provides a complete, AI-powered framework for managing software releases following Agile methodologies. Five specialized agents—each named after legendary Vietnamese strategists—work together to orchestrate releases from planning through retrospective.

### Core Philosophy

- **Quality over speed**: Never compromise safety for velocity
- **Transparency**: Communicate early and often
- **Data-driven decisions**: Rely on metrics, not opinions
- **Blameless culture**: Focus on processes, not people
- **Continuous improvement**: Every release teaches us something

### Key Features

✅ **Comprehensive Planning**: AI-guided release planning with versioning, changelog generation, and scope analysis
✅ **Quality Gates**: Automated validation across testing, security, performance, and documentation
✅ **Deployment Strategies**: Support for Blue-Green, Canary, Rolling, Feature Flags, and Recreate patterns
✅ **Risk Management**: Proactive identification and mitigation of deployment risks
✅ **Rollback Procedures**: Emergency rollback protocols with clear decision criteria
✅ **Communication Support**: Draft announcements, status updates, and incident reports
✅ **Learning Culture**: Structured retrospectives to continuously improve

---

## When to Use This Pack

### Perfect For

- **Agile teams** releasing software regularly (sprints, monthly, quarterly)
- **DevOps teams** seeking to standardize and improve release processes
- **Growing teams** moving from ad-hoc to structured release management
- **Teams struggling with** deployment anxiety, frequent rollbacks, or production incidents
- **Organizations** wanting to reduce release risk and increase predictability

### Use Cases

| Release Type | Workflow | Typical Use Case |
|--------------|----------|------------------|
| **Standard Release** | `standard-release.yaml` | Regular minor/patch releases with new features and bug fixes |
| **Hotfix Release** | `hotfix-release.yaml` | Critical production fixes requiring fast deployment (2-8 hours) |
| **Major Release** | `major-release.yaml` | Breaking changes, architectural updates, major versions with migration |

---

## Quick Start

### 1. Start a Standard Release

```bash
# Activate the Release Manager agent
*agent release-manager

# Choose your planning approach:

# Option A: Manual guided workflow (recommended for first-time users)
*plan

# Option B: Template-driven workflow (BMAD interactive elicitation)
*create-plan
```

**Two Planning Approaches:**

**`*plan`** - **Manual Guided Workflow** (9-phase process)
- Step-by-step guidance through each phase
- Custom logic for git analysis and scope analysis
- Interactive questions and recommendations
- Best for: Teams that need flexibility and detailed guidance

**`*create-plan`** - **Template-Driven Workflow** (Interactive elicitation)
- Section-by-section document creation
- BMAD universal elicitation pattern (1-9 options menu)
- Structured interactive workflow
- Best for: Teams familiar with BMAD document creation patterns

Both approaches guide you through:
- Determining version number (SemVer or CalVer)
- Analyzing scope
- Generating changelog
- Writing release notes
- Planning deployment
- Setting timeline

*Both generate the same comprehensive release plan document.*

### 2. Follow the Workflow

```bash
# Or run the complete standard release workflow
*workflow standard-release
```

The workflow orchestrates all agents automatically:
1. **Planning** → Release Manager + Scope Analyzer
2. **Quality Validation** → Quality Gatekeeper
3. **Deployment Preparation** → Deployment Coordinator
4. **Deployment Execution** → Deployment Coordinator
5. **Monitoring** → Release Manager
6. **Retrospective** → Release Manager

### 3. Get Help Anytime

```bash
# Each agent provides help
*agent release-manager
*help

# View available workflows
*workflows

# Access tasks directly
*task create-release-plan
```

---

## Meet Your Team

Five specialized AI agents, each named after legendary Vietnamese strategists, work together to manage your releases:

### 🚀 Trần Hưng Đạo - Release Manager

**The Orchestrator**

> Named after the legendary Vietnamese general who defeated Mongol invasions through strategic planning and coordination.

- **Role**: Primary coordinator for entire release lifecycle
- **Responsibilities**: Release planning, monitoring, retrospectives, decision-making
- **When to call**: Starting a release, monitoring deployment, facilitating retrospectives
- **Commands**: `*plan`, `*create-plan`, `*monitor`, `*retrospective`, `*status`

**Example**:
```bash
*agent release-manager

# Manual guided workflow (9-phase step-by-step)
*plan

# OR template-driven workflow (interactive elicitation)
*create-plan
```

---

### 🔍 Nguyễn Trãi - Scope Analyzer

**The Strategist**

> Named after the brilliant Vietnamese strategist and scholar known for strategic thinking and careful planning.

- **Role**: Strategic scope analysis and recommendations
- **Responsibilities**: Analyze completed work, assess readiness, recommend inclusion/deferral
- **When to call**: Determining what should go into a release
- **Commands**: `*analyze`, `*recommend`, `*status`

**Example**:
```bash
*agent scope-analyzer
*analyze  # Analyze scope for v2.1.0
```

---

### ✅ Lý Thường Kiệt - Quality Gatekeeper

**The Guardian**

> Named after the legendary general known for defensive strategy and protecting the nation's borders.

- **Role**: Quality standards guardian
- **Responsibilities**: Validate quality gates, make go/no-go recommendations, protect production
- **When to call**: Before deployment, validating quality standards
- **Commands**: `*validate`, `*status`, `*report`

**Example**:
```bash
*agent quality-gatekeeper
*validate  # Run comprehensive quality gates
```

---

### 🎯 Võ Nguyên Giáp - Deployment Coordinator

**The Commander**

> Named after the master military strategist known for coordinating complex operations.

- **Role**: Deployment operations commander
- **Responsibilities**: Plan deployment strategy, execute deployments, coordinate rollbacks
- **When to call**: Planning deployment, executing deployment, emergency rollback
- **Commands**: `*plan`, `*execute`, `*rollback`, `*status`

**Example**:
```bash
*agent deployment-coordinator
*plan  # Create deployment runbook
*execute  # Execute deployment
```

---

### 📣 Phan Bội Châu - Communication Specialist

**The Communicator**

> Named after the renowned revolutionary, scholar, and writer known for eloquent and strategic communication.

- **Role**: Release communications strategist
- **Responsibilities**: Draft announcements, status updates, incident reports, stakeholder communications
- **When to call**: Need release announcement, status update, incident communication
- **Commands**: `*draft`, `*review`, `*template`

**Example**:
```bash
*agent communication-specialist
*draft  # Draft release announcement
```

---

## Workflows

### Standard Release Workflow

**Duration**: 3-5 days
**For**: Regular minor/patch releases

**Phases**:
1. **Planning** (1-2 days): Comprehensive release planning with scope analysis
2. **Quality Validation** (2-4 hours): All quality gates validated
3. **Deployment Preparation** (2-3 hours): Deployment runbook and team briefing
4. **Deployment Execution** (1-3 hours): Execute deployment
5. **Post-Deployment Monitoring** (24-48 hours): Intensive monitoring
6. **Retrospective** (60-90 min): Learn and improve

```bash
*workflow standard-release
```

---

### Hotfix Release Workflow

**Duration**: 2-8 hours
**For**: Critical production fixes

**Phases**:
1. **Rapid Assessment** (30-60 min): Determine if hotfix warranted
2. **Focused Development** (1-3 hours): Implement and test fix
3. **Expedited Quality Check** (30-60 min): Critical gates only
4. **Rapid Deployment** (30-90 min): Deploy fix quickly
5. **Intensive Monitoring** (4-8 hours): Close monitoring
6. **Post-Hotfix Activities** (1-2 hours): Documentation and post-mortem

```bash
*workflow hotfix-release
```

---

### Major Release Workflow

**Duration**: 4-12 weeks
**For**: Breaking changes, major versions

**Phases**:
1. **Strategic Planning** (1-4 weeks): Vision, breaking changes, deprecation
2. **Migration Preparation** (2-4 weeks): Migration guides, beta program
3. **Beta Releases** (4-8 weeks): Beta 1, Beta 2-N, Release Candidates
4. **Comprehensive Planning** (1-2 weeks): Final release planning
5. **Intensive Quality Validation** (1-2 weeks): Exhaustive quality checks
6. **Staged Deployment** (1-2 weeks): Internal → Beta → Gradual → Full
7. **Extended Monitoring** (2-4 weeks): Migration support
8. **Retrospective** (1 week): Major release learning

```bash
*workflow major-release
```

---

## What's Included

### 📁 Directory Structure

```
bmad-release-management/
├── agents/                           # 5 specialized agents
│   ├── release-manager.md           # Trần Hưng Đạo - Orchestrator
│   ├── scope-analyzer.md            # Nguyễn Trãi - Strategist
│   ├── quality-gatekeeper.md        # Lý Thường Kiệt - Guardian
│   ├── deployment-coordinator.md    # Võ Nguyên Giáp - Commander
│   └── communication-specialist.md  # Phan Bội Châu - Communicator
│
├── workflows/                        # 3 end-to-end workflows
│   ├── standard-release.yaml        # Regular releases (3-5 days)
│   ├── hotfix-release.yaml          # Emergency fixes (2-8 hours)
│   └── major-release.yaml           # Breaking changes (4-12 weeks)
│
├── tasks/                           # 8 actionable tasks
│   ├── create-release-plan.md      # Comprehensive release planning
│   ├── analyze-scope.md            # Scope analysis and recommendations
│   ├── run-quality-gates.md        # Quality validation across all dimensions
│   ├── plan-deployment.md          # Deployment strategy and runbook creation
│   ├── execute-deployment.md       # Step-by-step deployment execution
│   ├── monitor-release.md          # 24-48 hour monitoring protocols
│   ├── conduct-retrospective.md    # Structured learning sessions
│   └── rollback-release.md         # Emergency rollback procedures
│
├── templates/                       # 1 comprehensive template
│   └── release-plan.md             # All-in-one release plan document
│
├── checklists/                      # 4 validation checklists
│   ├── pre-release-checklist.md    # Quality gates validation
│   ├── deployment-checklist.md     # Deployment execution steps
│   ├── post-deployment-checklist.md # Post-deployment verification
│   └── rollback-checklist.md       # Rollback procedures
│
├── data/                            # 4 knowledge base files
│   ├── release-management-kb.md    # Philosophy, principles, best practices
│   ├── versioning-strategies.md    # SemVer, CalVer, version numbering
│   ├── changelog-conventions.md    # Keep a Changelog, Conventional Commits
│   └── deployment-patterns.md      # Blue-Green, Canary, Rolling, etc.
│
├── config.yaml                      # Pack metadata
└── README.md                        # This file
```

### 📚 Total Content

- **5 Agents**: ~20,000 words of agent definitions
- **3 Workflows**: Comprehensive orchestration
- **8 Tasks**: ~40,000 words of step-by-step guides
- **1 Template**: All-in-one release plan
- **4 Checklists**: Validation and execution
- **4 Knowledge Base Files**: ~20,000 words of best practices

---

## Example Usage

### Scenario 1: Planning a Standard Release

```
You: "We need to plan v2.1.0 release"

*agent release-manager
*plan

Trần Hưng Đạo: "Let's create a comprehensive release plan for v2.1.0.

First, what are the main goals for this release?"

You: "Add OAuth authentication, dark mode, and CSV export"

Trần Hưng Đạo: "Excellent! Those are three solid features. Based on these features:
- Recommended version: v2.1.0 (minor version - new features, backwards-compatible)
- I'll generate a changelog from git history
- Write user-friendly release notes
- Analyze scope with the Scope Analyzer

Let me call in Nguyễn Trãi to analyze the scope..."

[Scope Analyzer analyzes git history, recommends inclusions/deferrals]

[Release Manager generates changelog and release notes]

[Communication Specialist drafts announcement]

Result: Complete release plan saved to docs/release/v2.1.0-release-plan.md
```

---

### Scenario 2: Quality Gate Validation

```
You: "Are we ready to deploy v2.1.0?"

*agent quality-gatekeeper
*validate

Lý Thường Kiệt: "I'll conduct comprehensive quality assessment for v2.1.0...

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
QUALITY GATE ASSESSMENT - v2.1.0
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1️⃣ TEST COVERAGE & RESULTS ✅ PASS
   Unit Test Coverage:     85% (threshold: 80%) ✅
   Integration Tests:      All 127 passing ✅
   E2E Tests:             All 45 passing ✅

2️⃣ SECURITY ASSESSMENT ✅ PASS
   SAST Scan:             0 critical, 0 high ✅
   DAST Scan:             0 critical, 0 high ✅
   Dependencies:          1 medium vuln (dev-only) ⚠️

3️⃣ PERFORMANCE VALIDATION ✅ PASS
   Response Time p95:     420ms (baseline: 450ms) ✅
   Performance IMPROVED by 7% ⬆️

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
OVERALL ASSESSMENT: ✅ GO FOR DEPLOYMENT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

All critical gates passed. I recommend proceeding with deployment."
```

---

### Scenario 3: Emergency Hotfix

```
User: "Production is down! Users can't log in!"

*workflow hotfix-release

[Workflow guides through rapid assessment]

Trần Hưng Đạo: "Assessing severity... this is a P0 critical issue.
Hotfix is warranted. Creating hotfix plan for v2.1.1..."

[Quick development, testing, quality check]

Võ Nguyên Giáp: "Deploying hotfix v2.1.1 using Blue-Green for instant rollback...
✅ Deployed in 8 minutes
✅ Login functionality restored
✅ Error rate normalized"

Phan Bội Châu: "Incident communication sent to users:
'Login issue resolved. All systems operational. We apologize for the 12-minute
disruption.'"

Result: Production restored in under 2 hours, post-mortem scheduled
```

---

### Scenario 4: Major Release with Breaking Changes

```
You: "We're planning v3.0.0 with breaking API changes"

*workflow major-release

[12-week comprehensive process]

Phase 1-2: Strategic planning and migration guide creation
Phase 3: Beta releases (v3.0.0-beta.1, beta.2, RC)
Phase 4-5: Final planning and intensive quality validation
Phase 6: Staged deployment (Internal → 5% → 25% → 50% → 100%)
Phase 7: Extended monitoring and migration support
Phase 8: Retrospective and celebration

Result: Successful major release with >95% user migration,
minimal support burden, positive user feedback
```

---

## Best Practices

### 1. Release Planning

- **Start early**: Begin planning 1-2 weeks before deployment
- **Analyze scope objectively**: Use Scope Analyzer to make inclusion/deferral decisions based on readiness, not pressure
- **Version consistently**: Follow SemVer or CalVer consistently (see `data/versioning-strategies.md`)
- **Write user-focused release notes**: Explain value, not just technical changes

### 2. Quality Gates

- **Never skip critical gates**: Security, core functionality, data integrity are non-negotiable
- **Automate validation**: Integrate quality gates into CI/CD pipeline
- **Document acceptable risks**: If deploying with known issues, document explicitly
- **Test migrations thoroughly**: Database and data migrations should be tested with production-scale data

### 3. Deployment

- **Choose the right strategy**: Blue-Green for instant rollback, Canary for gradual rollout, Rolling for cost-effectiveness
- **Always have rollback plan**: Test rollback procedures before deployment
- **Monitor intensively**: First 4 hours are critical—watch metrics every 15-30 minutes
- **Communicate proactively**: Update stakeholders every 30 minutes during deployment

### 4. Rollback

- **Have clear criteria**: Define rollback triggers before deployment (error rate >X%, functionality broken)
- **Don't hesitate**: Better to rollback quickly than hope issue resolves itself
- **Stay calm**: Rollbacks are safety mechanisms, not failures
- **Learn from incidents**: Every rollback is a learning opportunity

### 5. Communication

- **Transparency builds trust**: Be honest about issues and timelines
- **Tailor to audience**: Executives need business impact, engineers need technical details
- **Communicate early**: Don't wait for complete information—update as you learn
- **Celebrate successes**: Recognize team effort and successful releases

### 6. Continuous Improvement

- **Never skip retrospectives**: Schedule within 2-3 days of deployment
- **Create actionable items**: Specific improvements with owners and deadlines
- **Track metrics over time**: Lead time, deployment frequency, incident rate, rollback rate
- **Share learnings**: Document for future releases and new team members

---

## Installation

### Prerequisites

- BMAD Core installed
- Access to git repository
- Deployment infrastructure (K8s, Docker, etc.)
- Monitoring tools (optional but recommended)

### Installation Steps

1. **Clone or copy** the `bmad-release-management` folder to your `expansion-packs/` directory

2. **Activate an agent** to get started:
   ```bash
   *agent release-manager
   ```

3. **Run a workflow** for guided release process:
   ```bash
   *workflow standard-release
   ```

4. **Customize** templates and checklists for your organization:
   - Edit `templates/release-plan.md` with your organization's specifics
   - Adjust quality gate thresholds in `checklists/pre-release-checklist.md`
   - Customize deployment patterns in `data/deployment-patterns.md`

---

## Configuration

### Versioning Strategy

Choose your versioning approach in `data/versioning-strategies.md`:
- **SemVer** (Semantic Versioning): v2.1.0 (MAJOR.MINOR.PATCH)
- **CalVer** (Calendar Versioning): v2025.01.0 (YYYY.MM.MINOR)

### Deployment Patterns

Configure your preferred deployment strategy in `data/deployment-patterns.md`:
- **Blue-Green**: Zero downtime, instant rollback (requires 2x infrastructure)
- **Canary**: Gradual rollout with monitoring (5% → 25% → 50% → 100%)
- **Rolling**: Cost-effective, brief disruption
- **Feature Flags**: Decouple deployment from release
- **Recreate**: Simple, downtime acceptable

### Quality Gates

Customize quality thresholds in `checklists/pre-release-checklist.md`:
- Test coverage: 70-80%
- Security: 0 critical/high vulnerabilities
- Performance: ±10% of baseline
- Documentation: Complete for user-facing changes

---

## Support & Contributions

### Getting Help

- Each agent has built-in help: `*agent <name>` then `*help`
- Comprehensive task guides: `*task <name>`
- Knowledge base: `data/*.md` files

### Contributing

Found a better practice? Improved a template? Contributions welcome!

1. Test improvements in your environment
2. Document changes clearly
3. Share learnings in retrospectives
4. Submit improvements back to pack

---

## License

Part of the BMAD (Build, Maintain, and Deploy) Method Minions project.

---

## Acknowledgments

**Named after Vietnamese historical figures:**
- **Trần Hưng Đạo** (1228-1300): Legendary general who defeated Mongol invasions
- **Nguyễn Trãi** (1380-1442): Brilliant strategist, scholar, and poet
- **Lý Thường Kiệt** (1019-1105): General known for defensive strategy and protection
- **Võ Nguyên Giáp** (1911-2013): Master military strategist of the 20th century
- **Phan Bội Châu** (1867-1940): Revolutionary, scholar, and eloquent writer

These legendary figures inspire the strategic thinking, careful planning, and excellent execution embodied by the release management agents.

---

## Quick Reference

### Common Commands

```bash
# Start release planning
*agent release-manager
*plan

# Analyze scope
*agent scope-analyzer
*analyze

# Validate quality
*agent quality-gatekeeper
*validate

# Plan deployment
*agent deployment-coordinator
*plan

# Draft communications
*agent communication-specialist
*draft

# Run full workflow
*workflow standard-release
*workflow hotfix-release
*workflow major-release
```

### File Locations

- **Release Plans**: `docs/release/v{version}-release-plan.md`
- **Checklists**: `checklists/*.md`
- **Knowledge Base**: `data/*.md`
- **Templates**: `templates/release-plan.md`

---

**Ready to transform your release process? Activate the Release Manager and start planning your next release!**

```bash
*agent release-manager
```
