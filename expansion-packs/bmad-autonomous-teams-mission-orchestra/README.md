# Autonomous Teams Mission Orchestra Pack

**Orchestrate autonomous teams through federated repository development while maintaining team independence.**

---

## Overview

This expansion pack extends BMAD Core to support **cross-team coordination** in federated repository architectures (Git submodules, monorepos, microservices). It provides specialized agents, workflows, and templates for managing missions that span multiple autonomous teams.

### Use Cases

- Coordinating mobile, backend, AI, data teams in federated repositories
- Managing microservices developed by different teams
- Planning features requiring cross-functional collaboration
- Maintaining team autonomy while ensuring mission alignment

### What You Get

- **5 Orchestration Agents**: Mission PM, Mission PO, Triage Master, Mission Orchestrator, Integration Specialist
- **Mission-Level Planning**: Cross-team PRDs with RACI matrices
- **Formal Alignment Process**: Team commitment ceremonies
- **Automated Triage**: Route bugs/enhancements/features to correct teams
- **Integration Contracts**: API contract design and validation
- **Team Handoffs**: Decompose missions into team-specific work

---

## Prerequisites

- **Node.js** ≥ 18, **npm** ≥ 9
- **BMAD Core** (this pack extends Core - cannot work standalone)

### Core Dependencies

This pack requires these BMAD Core components:

| Component | Purpose |
|-----------|---------|
| `analyst` agent | Creating project briefs |
| `pm` agent | PRD creation |
| `architect` agent | System design |
| `po` agent | Document sharding |
| `create-doc` task | Template processing |

> ⚠️ **Must install BMAD Core + this pack together**

---

## Installation

### Step 1: Clone BMAD-METHOD

```bash
git clone https://github.com/bmad-code-org/BMAD-METHOD.git
cd BMAD-METHOD
```

### Step 2: Add This Pack

Copy `bmad-autonomous-teams-mission-orchestra` to `expansion-packs/`:

```bash
# From a zip/download
unzip bmad-autonomous-teams-mission-orchestra.zip -d expansion-packs/

# Or clone from your repository
cd expansion-packs
git clone <your-pack-repo> bmad-autonomous-teams-mission-orchestra
cd ..
```

### Step 3: Install BMAD with Pack

```bash
npm install
npm run install:bmad
```

**During installation:**

1. Choose: **"Install BMAD Core + Expansion Packs"** (NOT "Expansion Packs Only")
2. Select: **"Autonomous Teams Mission Orchestra"**
3. Specify your target project directory

The installer will integrate both BMAD Core and this pack into your project.

### Step 4: Configure Your Teams

Edit `.bmad-core/data/orchestra-config.yaml`:

```yaml
teams:
  - id: mobile
    name: Mobile Team
    repositories: [mobile-app]
    contacts:
      lead: mobile-lead@example.com
      slack_channel: "#team-mobile"

  - id: backend
    name: Backend Team
    repositories: [api-service]
    contacts:
      lead: backend-lead@example.com
      slack_channel: "#team-backend"

  # Add your teams...

integrations:
  - id: mobile_backend_api
    name: Mobile to Backend API
    type: rest_api
    provider: backend
    consumers: [mobile]
    specification:
      format: openapi
      location: docs/api/mobile-api.yaml
```

---

## Quick Start Guide

### Scenario: New Feature Spanning Multiple Teams

#### 1. Triage the Request

```bash
@triage-master triage "Add payment processing to mobile and web apps"
```

**Result:** Classified as FEATURE requiring Mission Planning (affects 3+ teams)

#### 2. Create Foundation

```bash
# Start with project brief
@analyst create-project-brief

# Create Mission PRD from brief (using Mission PM)
@mission-pm create-mission-prd
```

**Mission PRD includes:**
- Shared goals across teams
- Cross-team epics
- Team responsibility matrix (RACI)
- Integration points

#### 3. Align Teams

```bash
@mission-orchestrator facilitate-alignment
```

**Alignment meeting:**
- All team leads review Mission PRD
- Discuss dependencies
- Make formal commitments
- Document decisions

**Output:** Aligned Mission PRD with team commitments

#### 4. Decompose to Teams

```bash
# Using Mission PO for cross-team decomposition
@mission-po shard-mission-to-teams
```

**Creates team handoff documents:**
- `docs/teams/mobile/handoff-{mission}.md`
- `docs/teams/backend/handoff-{mission}.md`
- Each contains team-specific epics, dependencies, contracts

#### 5. Create Team PRDs

```bash
# Mission PM creates focused PRDs for each team
@mission-pm create-team-prd
> Team: mobile
> Creates: docs/teams/mobile/prd-{mission}.md

@mission-pm create-team-prd
> Team: backend
> Creates: docs/teams/backend/prd-{mission}.md
```

#### 6. Team Execution

Each team in their repository:

```bash
# Standard BMAD dev workflow with team PRD
@sm create next story  # Using team's PRD
@dev implement story
@qa review story
```

Teams work autonomously with clear integration contracts.

---

## The Five Orchestration Agents

### 🎯 Mission PM (Dao)

**Strategic mission orchestrator for cross-team product initiatives**

```bash
@mission-pm create-mission-prd    # Create cross-team mission PRD
@mission-pm facilitate-alignment   # Run team alignment ceremony
@mission-pm define-raci           # Create RACI matrix
@mission-pm orchestrate-mission   # Execute full mission workflow
@mission-pm create-team-prd       # Create team PRD from handoff
```

**Core Focus:**
- Cross-team PRD creation with shared goals
- RACI matrix for clear responsibilities
- Team alignment facilitation
- Team-specific PRD generation from handoffs
- Mission orchestration workflow

---

### 🎭 Mission PO (Kiet)

**Mission decomposer who breaks complex initiatives into team-specific work**

```bash
@mission-po shard-mission-to-teams  # Decompose mission PRD by team
@mission-po route-work              # Route work to appropriate team
@mission-po create-team-handoff     # Generate team-specific handoff
```

**Core Focus:**
- Decompose mission PRDs by team
- Route work items to correct teams
- Create team-specific handoff documents

---

### 🚦 Triage Master

**Routes incoming work to correct teams and workflows**

```bash
@triage-master triage {issue}
@triage-master classify {description}
@triage-master identify-team {work-item}
```

**Handles:**
- Bugs → Severity assessment → Team backlog
- Enhancements → Product backlog
- Features → Mission planning

---

### 🎭 Mission Orchestrator

**Coordinates cross-team missions**

```bash
@mission-orchestrator facilitate-alignment
@mission-orchestrator track-commitments
@mission-orchestrator mission-status
@mission-orchestrator handoff-to-teams
```

**Manages:**
- Alignment meetings
- Team commitments
- Dependencies
- Integration milestones

---

### 🔌 Integration Specialist

**Designs API contracts between teams**

```bash
@integration-specialist design-contract {service}
@integration-specialist validate-contract
@integration-specialist check-breaking-changes
```

**Provides:**
- API contract design (REST/GraphQL/gRPC)
- Integration test scenarios
- Breaking change analysis
- Mock service generation

---

## Workflows

### Mission Planning Workflow

**From idea to team execution in 2-3 weeks**

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         MISSION PLANNING WORKFLOW                        │
└─────────────────────────────────────────────────────────────────────────┘

┌────────────────┐
│   New Idea /   │
│  Feature Request│
└────────┬───────┘
         │
         ▼
┌─────────────────────────────────────────────────────────────────────────┐
│  PHASE 1: DISCOVERY (2-3 days)                                          │
├─────────────────────────────────────────────────────────────────────────┤
│  @analyst create-project-brief                                          │
│  • Brainstorm with stakeholders                                         │
│  • Identify affected teams                                              │
│  • Draft problem statement                                              │
│                                                                          │
│  OUTPUT: project-brief.md                                               │
└────────┬────────────────────────────────────────────────────────────────┘
         │
         ▼
┌─────────────────────────────────────────────────────────────────────────┐
│  PHASE 2: DEFINITION (3-5 days)                                         │
├─────────────────────────────────────────────────────────────────────────┤
│  @mission-pm create-mission-prd                                         │
│  • Define shared goals across teams                                     │
│  • Create RACI matrix                                                   │
│  • Identify integration points                                          │
│                                                                          │
│  @architect design-system                                               │
│  • Technical architecture                                               │
│  • API contracts                                                        │
│  • Data flows                                                           │
│                                                                          │
│  OUTPUT: mission-prd.md, architecture-design.md                         │
└────────┬────────────────────────────────────────────────────────────────┘
         │
         ▼
┌─────────────────────────────────────────────────────────────────────────┐
│  PHASE 3: ALIGNMENT (1 week)                                            │
├─────────────────────────────────────────────────────────────────────────┤
│  @mission-orchestrator facilitate-alignment                             │
│  • Schedule alignment meeting (90 min)                                  │
│  • All team leads review Mission PRD                                    │
│  • Discuss dependencies & constraints                                   │
│  • Teams make formal commitments:                                       │
│    ✓ Full Commit                                                        │
│    ⚠ Conditional Commit (with conditions)                               │
│    ✗ Cannot Commit (with reasons)                                       │
│                                                                          │
│  @integration-specialist design-contracts                               │
│  • Define API specifications                                            │
│  • Create integration tests                                             │
│                                                                          │
│  OUTPUT: aligned-mission-prd.md, alignment-notes.md, api-contracts/     │
└────────┬────────────────────────────────────────────────────────────────┘
         │
         ▼
┌─────────────────────────────────────────────────────────────────────────┐
│  PHASE 4: DECOMPOSITION & TEAM PRDs (2-3 days)                          │
├─────────────────────────────────────────────────────────────────────────┤
│  @mission-po shard-mission-to-teams                                     │
│  • Decompose Mission PRD by team                                        │
│  • Create team-specific handoff docs                                    │
│                                                                          │
│  @mission-pm create-team-prd (for each team)                            │
│  • Transform handoffs into team PRDs                                    │
│  • Focus on team-specific requirements                                  │
│                                                                          │
│  OUTPUT: docs/teams/{team-id}/handoff-{mission}.md                      │
│          docs/teams/{team-id}/prd-{mission}.md                          │
└────────┬────────────────────────────────────────────────────────────────┘
         │
         ▼
┌─────────────────────────────────────────────────────────────────────────┐
│  PHASE 5: EXECUTION (variable duration)                                 │
├─────────────────────────────────────────────────────────────────────────┤
│  Each team in their own repository with their team PRD:                 │
│                                                                          │
│  @sm create stories      # From docs/teams/{team}/prd-{mission}.md      │
│  @dev implement features                                                │
│  @qa test & validate                                                    │
│                                                                          │
│  • Teams work autonomously                                              │
│  • Integration checkpoints every 2 weeks                                │
│  • Weekly sync meetings                                                 │
│                                                                          │
│  OUTPUT: Working features in each team's repository                     │
└─────────────────────────────────────────────────────────────────────────┘
```

### Triage Routing Workflow

**Classify and route work in < 4 hours**

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        TRIAGE ROUTING WORKFLOW                           │
└─────────────────────────────────────────────────────────────────────────┘

                          ┌─────────────┐
                          │  Work Item  │
                          │   Incoming  │
                          └──────┬──────┘
                                 │
                                 ▼
                    ┌────────────────────────┐
                    │  @triage-master triage │
                    │  Analyze & Classify    │
                    └────────────┬───────────┘
                                 │
                 ┌───────────────┼───────────────┐
                 │               │               │
                 ▼               ▼               ▼
         ┌─────────────┐ ┌──────────────┐ ┌───────────┐
         │     BUG     │ │ ENHANCEMENT  │ │  FEATURE  │
         │ (Broken)    │ │  (Improve)   │ │   (New)   │
         └──────┬──────┘ └──────┬───────┘ └─────┬─────┘
                │               │                 │
                │               │                 │
         ┌──────▼──────┐        │                 │
         │  Severity   │        │                 │
         │  Assessment │        │                 │
         └──────┬──────┘        │                 │
                │               │                 │
    ┌───────────┼──────────┐    │                 │
    │           │          │    │                 │
    ▼           ▼          ▼    ▼                 ▼
┌─────────┐ ┌────────┐ ┌─────────────┐    ┌──────────────┐
│CRITICAL │ │  HIGH  │ │MEDIUM / LOW │    │   Validate   │
│         │ │        │ │             │    │  Scope       │
└────┬────┘ └───┬────┘ └──────┬──────┘    └──────┬───────┘
     │          │             │                   │
     │          │             │          ┌────────┼────────┐
     │          │             │          │                 │
     ▼          ▼             ▼          ▼                 ▼
┌─────────────────────────────────┐  ┌──────────┐  ┌──────────────┐
│  ROUTE TO OWNING TEAM           │  │ Single   │  │  Multiple    │
│                                 │  │  Team    │  │   Teams      │
│  Pattern Matching:              │  └────┬─────┘  └──────┬───────┘
│  • "mobile|ios|android"         │       │               │
│    → Mobile Team                │       │               │
│  • "backend|api|service"        │       ▼               ▼
│    → Backend Team               │  ┌──────────┐  ┌─────────────┐
│  • "web|browser|portal"         │  │ Product  │  │   Mission   │
│    → Web Team                   │  │ Backlog  │  │  Planning   │
│  • "ai|ml|model"                │  └──────────┘  └─────────────┘
│    → AI Team                    │                       │
│  • "data|etl|analytics"         │                       │
│    → Data Team                  │                       ▼
│  • "deploy|ci|infrastructure"   │              Goto Mission
│    → DevOps Team                │              Planning Workflow
└─────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────┐
│  OUTPUTS:                                                                │
│  • Bugs → Team backlog with severity & SLA                              │
│  • Enhancements → Product backlog for prioritization                    │
│  • Features → Mission Planning Workflow (if cross-team)                 │
│  • Features → Team backlog (if single team)                             │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Configuration

### Team Structure

Edit `.bmad-core/data/orchestra-config.yaml`:

```yaml
teams:
  - id: {team-id}
    name: {Team Name}
    repositories: [{repo-names}]
    responsibilities:
      - {what this team builds}
    technologies:
      - {tech stack}
    contacts:
      lead: {team-lead-email}
      slack_channel: {slack-channel}
```

### Integration Points

```yaml
integrations:
  - id: {integration-id}
    type: rest_api|graphql|grpc|event_stream
    provider: {team-providing-api}
    consumers: [{teams-consuming-api}]
    specification:
      format: openapi|graphql_schema|protobuf
      location: {path-to-spec}
```

---

## Best Practices

1. **Always start with project brief** - Provides context for all teams
2. **Limit mission scope** - Keep missions focused, break large initiatives into smaller missions
3. **Make dependencies explicit** - Document what's needed, from whom, by when
4. **Use formal commitments** - Get written team confirmation, respect "cannot commit"
5. **Keep handoffs focused** - Each team gets only what they need
6. **Monitor integration points** - Track API contracts, SLAs, breaking changes

---

## Troubleshooting

### Missing Core Dependencies

**Problem:** "Agent not found" or "task not found" errors

**Fix:**
```bash
# Check if core agents exist
ls .bmad-core/agents/ | grep -E "analyst|pm|architect|po"

# If missing, reinstall
cd <BMAD-METHOD-directory>
npm run install:bmad
# Choose: "Install BMAD Core + Expansion Packs"
# Select: "Autonomous Teams Mission Orchestra"
```

**Common mistakes:**
- ❌ Selecting "Expansion Packs Only" (requires Core!)
- ✅ Select "Core + Expansion Packs"

### Teams Not Committing

**Problem:** Teams hesitant during alignment

**Solutions:**
- Review capacity realistically
- Reduce scope or extend timeline
- Break into smaller missions
- Document conditions clearly

### Integration Issues

**Problem:** APIs don't work when teams integrate

**Solutions:**
- Review contracts carefully
- Use contract testing
- Regular integration checkpoints
- Validate with Integration Specialist

---

## Support

- 💬 [BMAD Discord Community](https://discord.gg/gk8jAdXWmj)
- 📖 [BMAD Documentation](https://github.com/bmad-code-org/BMAD-METHOD/docs)
- 🐛 [Report Issues](https://github.com/bmad-code-org/BMAD-METHOD/issues)

---

## Version

**Pack Version:** 2.0.0
**BMAD Core Compatibility:** v1.0.0+
**License:** MIT

---

**Created for orchestrating autonomous teams in federated repositories.**
**Built on BMAD Method by BMadCode.**