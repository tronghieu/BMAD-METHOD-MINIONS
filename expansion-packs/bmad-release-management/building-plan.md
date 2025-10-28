# Building Plan: BMAD Release Management Expansion Pack

## Purpose
This document tracks the progress of building the Release Management expansion pack across multiple work sessions.

---

## High-Level Architecture Decisions

### Agents (5 total)
- ✅ **Release Manager** - Primary orchestrator (handles versioning, changelog, release notes, monitoring, retrospectives)
- ✅ **Scope Analyzer** - Determines what to include/exclude
- ✅ **Quality Gatekeeper** - Validates quality gates
- ✅ **Deployment Coordinator** - Plans and executes deployment
- ✅ **Communication Specialist** - Handles stakeholder communications

### Workflows (3 total)
- ✅ **standard-release** - Regular planned releases
- ✅ **hotfix-release** - Critical production fixes
- ✅ **major-release** - Breaking changes/major versions

### Templates (1 unified)
- ✅ **release-plan.md** - All-in-one document with sections: overview, scope, changelog, release notes, deployment plan, communications, monitoring, retrospective

### Tasks (8 total)
1. create-release-plan
2. analyze-scope
3. run-quality-gates
4. plan-deployment
5. execute-deployment
6. monitor-release
7. conduct-retrospective
8. rollback-release

### Checklists (4 total)
1. pre-release-checklist
2. deployment-checklist
3. post-deployment-checklist
4. rollback-checklist

### Data/Knowledge Base (4 files)
1. release-management-kb
2. versioning-strategies
3. changelog-conventions
4. deployment-patterns

---

## Build Order & Status

### Phase 1: Foundation ✅ COMPLETE
**Goal**: Create knowledge base and structural files

- [x] Create folder structure (agents/, workflows/, tasks/, templates/, checklists/, data/)
- [x] Write `data/release-management-kb.md`
- [x] Write `data/versioning-strategies.md`
- [x] Write `data/changelog-conventions.md`
- [x] Write `data/deployment-patterns.md`
- [x] Write `config.yaml` (metadata file)

**Current Status**: Complete (2025-10-28)
**Next Steps**: Completed - Move to Phase 2

---

### Phase 2: Checklists ✅ COMPLETE
**Goal**: Define concrete validation steps

- [x] Write `checklists/pre-release-checklist.md`
- [x] Write `checklists/deployment-checklist.md`
- [x] Write `checklists/post-deployment-checklist.md`
- [x] Write `checklists/rollback-checklist.md`

**Current Status**: Complete (2025-10-28)
**Dependencies**: Phase 1 (data files for reference)

---

### Phase 3: Templates ✅ COMPLETE
**Goal**: Create unified release plan template

- [x] Write `templates/release-plan.yaml` (YAML template matching story-tmpl.yaml pattern) ✅
  - Template metadata and workflow configuration
  - 11 major sections with subsections:
    - Release Overview
    - Scope
    - Changelog (Technical)
    - Release Notes (User-Facing)
    - Quality Assessment
    - Deployment Plan
    - Communications Plan
    - Monitoring Plan
    - Execution Log
    - Post-Release Monitoring
    - Retrospective
  - Owner/editors defined per section
  - Elicit flags for interactive sections
  - References to knowledge base and checklists
  - Workflow guidance and interactive principles

**Current Status**: Complete (2025-10-28, refactored in Session 3)
**Dependencies**: Phase 1 (knowledge base), Phase 2 (checklists to reference)

---

### Phase 4: Tasks ✅ COMPLETE
**Goal**: Define agent actions

- [x] Write `tasks/create-release-plan.md` ✅
- [x] Write `tasks/analyze-scope.md` ✅
- [x] Write `tasks/run-quality-gates.md` ✅
- [x] Write `tasks/plan-deployment.md` ✅
- [x] Write `tasks/execute-deployment.md` ✅
- [x] Write `tasks/monitor-release.md` ✅
- [x] Write `tasks/conduct-retrospective.md` ✅
- [x] Write `tasks/rollback-release.md` ✅

**Current Status**: Complete (2025-10-28)
**Dependencies**: Phase 1-3 (all foundation components)

---

### Phase 5: Agents ✅ COMPLETE
**Goal**: Define agent personas and capabilities

- [x] Write `agents/release-manager.md` → Trần Hưng Đạo (Release Management Orchestrator) ✅
- [x] Write `agents/scope-analyzer.md` → Nguyễn Trãi (Release Scope Strategist) ✅
- [x] Write `agents/quality-gatekeeper.md` → Lý Thường Kiệt (Quality Standards Guardian) ✅
- [x] Write `agents/deployment-coordinator.md` → Võ Nguyên Giáp (Deployment Operations Commander) ✅
- [x] Write `agents/communication-specialist.md` → Phan Bội Châu (Release Communications Strategist) ✅

**Current Status**: Complete (2025-10-28)
**Dependencies**: Phase 4 (tasks must exist to reference)

---

### Phase 6: Workflows ✅ COMPLETE
**Goal**: Define end-to-end processes

- [x] Write `workflows/standard-release.yaml` (Regular releases, 3-5 days, 6 phases) ✅
- [x] Write `workflows/hotfix-release.yaml` (Emergency fixes, 2-8 hours, 6 phases) ✅
- [x] Write `workflows/major-release.yaml` (Breaking changes, 4-12 weeks, 8 phases) ✅

**Current Status**: Complete (2025-10-28)
**Dependencies**: Phase 5 (agents must exist to orchestrate)

---

### Phase 7: Documentation ✅ COMPLETE
**Goal**: Complete pack documentation

- [x] Write `README.md` with: ✅
  - Pack overview
  - When to use this pack
  - Quick start guide
  - Agent descriptions (all 5 with Vietnamese names)
  - Workflow descriptions (all 3 workflows)
  - Example usage (4 scenarios)
  - Installation instructions
  - Best practices
  - Quick reference

**Current Status**: Complete (2025-10-28)
**Dependencies**: All previous phases

---

### Phase 8: Testing & Refinement ⬜ NOT STARTED
**Goal**: Validate pack works as intended

- [ ] Test standard-release workflow end-to-end
- [ ] Test hotfix-release workflow
- [ ] Refine based on real usage
- [ ] Update documentation with learnings

**Current Status**: Not started
**Dependencies**: Phase 7 (complete pack)

---

## Session Log

### Session 1 - 2025-10-28
**Activities**:
- Brainstormed expansion pack concept
- Simplified from 10 agents to 5 agents
- Consolidated templates into single release-plan.md
- Created building-plan.md document
- **COMPLETED Phase 1**: Created folder structure and all 4 knowledge base files
  - release-management-kb.md (philosophy, principles, types, risk management, quality gates, monitoring)
  - versioning-strategies.md (SemVer, CalVer, versioning strategies, pre-release versions, git integration)
  - changelog-conventions.md (Keep a Changelog, Conventional Commits, writing guidelines, automation)
  - deployment-patterns.md (Blue-Green, Canary, Rolling, Feature Flags, database migrations, health checks)
- **COMPLETED Phase 2**: Created all 4 checklists
  - pre-release-checklist.md (comprehensive quality gates: testing, security, performance, docs, compliance)
  - deployment-checklist.md (step-by-step deployment execution with multiple deployment patterns)
  - post-deployment-checklist.md (24-48 hour verification with metrics tracking)
  - rollback-checklist.md (emergency rollback procedures with decision tree)
- **COMPLETED Phase 3**: Created unified release-plan template
  - templates/release-plan.md (11 major sections, comprehensive with LLM guidance)
  - Includes: Overview, Scope, Changelog, Release Notes, Quality Assessment, Deployment Plan, Communications, Monitoring, Execution Log, Post-Release Monitoring, Retrospective
  - Built with template variables ({{placeholders}}) and [[LLM: instructions]] for agent guidance
  - NOTE: Later refactored to YAML format in Session 3
- **COMPLETED Phase 4**: Created all 8 tasks
  - tasks/create-release-plan.md (comprehensive 9-phase planning process with Release Manager)
  - tasks/analyze-scope.md (systematic scope analysis with inclusion/deferral recommendations)
  - tasks/run-quality-gates.md (comprehensive quality validation across all dimensions)
  - tasks/plan-deployment.md (deployment strategy selection and detailed planning)
  - tasks/execute-deployment.md (step-by-step deployment execution with multiple patterns)
  - tasks/monitor-release.md (24-48 hour monitoring with hourly/daily check-ins)
  - tasks/conduct-retrospective.md (structured learning and continuous improvement)
  - tasks/rollback-release.md (emergency rollback procedures for all deployment patterns)
- **STARTED Phase 5**: Created first agent
  - agents/release-manager.md (primary orchestrator with YAML header, full persona definition)
  - Includes: Activation instructions, commands, dependencies, decision frameworks, interaction patterns
- Created config.yaml with pack metadata

**Decisions Made**:
- Release Manager handles versioning, changelog, release notes, monitoring, retrospectives (not separate agents)
- Single unified template instead of 7 separate templates
- Focus on 3 core workflows (standard, hotfix, major)
- Comprehensive checklists that cover all quality gates and procedures
- Detailed knowledge base provides foundation for all agents
- Template uses variable substitution similar to BMAD Design Thinking pack
- Tasks are comprehensive guides (3,000-5,000 words each) with step-by-step processes
- Agent definitions follow BMAD pattern with YAML headers and activation instructions

**Progress**:
- Phase 1 ✅ Complete (4 files)
- Phase 2 ✅ Complete (4 files)
- Phase 3 ✅ Complete (1 file)
- Phase 4 ✅ Complete (8 files)
- Phase 5 🔄 In Progress (1 of 5 agents complete)

**Word Count Estimate**: ~65,000 words created across all files

**Files Created**: 18 files total
- 4 knowledge base files
- 4 checklists
- 1 template (comprehensive, multi-section markdown - later refactored to YAML in Session 3)
- 8 tasks (each 3,000-5,000 words)
- 1 agent definition

**Next Session Goals**:
- Complete Phase 5: Write remaining 4 agents
  - scope-analyzer.md
  - quality-gatekeeper.md
  - deployment-coordinator.md
  - communication-specialist.md
- Complete Phase 6: Design 3 workflows
  - standard-release.yaml
  - hotfix-release.yaml
  - major-release.yaml
- Complete Phase 7: Write README.md
- Test and validate pack structure

---

### Session 2 - 2025-10-28 (Continuation)
**Activities**:
- Updated all agent names to Vietnamese historical figures
- **COMPLETED Phase 5**: Created all 5 agents with Vietnamese names
  - agents/release-manager.md → Trần Hưng Đạo (legendary general and strategist)
  - agents/scope-analyzer.md → Nguyễn Trãi (brilliant strategist and scholar)
  - agents/quality-gatekeeper.md → Lý Thường Kiệt (general known for defensive strategy)
  - agents/deployment-coordinator.md → Võ Nguyên Giáp (master of coordinating operations)
  - agents/communication-specialist.md → Phan Bội Châu (revolutionary writer and communicator)
  - Each agent: ~5,000-6,000 words with YAML headers, personas, interaction patterns, decision frameworks
- **COMPLETED Phase 6**: Created all 3 workflows
  - workflows/standard-release.yaml (regular releases, 3-5 days, 6 phases)
  - workflows/hotfix-release.yaml (emergency fixes, 2-8 hours, 6 phases)
  - workflows/major-release.yaml (breaking changes, 4-12 weeks, 8 phases)
  - Each workflow: ~2,000-4,000 words with detailed phase definitions, gates, timelines
- **COMPLETED Phase 7**: Created comprehensive README.md
  - Complete pack documentation (~5,000 words)
  - Overview, quick start, agent introductions
  - Workflow descriptions, example usage
  - Best practices, installation, configuration
  - Quick reference guide

**Decisions Made**:
- Vietnamese historical figures selected for authentic representation
- Workflows follow YAML format with comprehensive phase definitions
- README structured for both quick start and comprehensive reference
- Tool-agnostic approach allows teams to use any CI/CD, monitoring tools
- Support both SemVer and CalVer (teams choose based on needs)

**Progress**:
- Phase 1 ✅ Complete (4 knowledge base files)
- Phase 2 ✅ Complete (4 checklists)
- Phase 3 ✅ Complete (1 template)
- Phase 4 ✅ Complete (8 tasks)
- Phase 5 ✅ Complete (5 agents, all with Vietnamese names)
- Phase 6 ✅ Complete (3 workflows)
- Phase 7 ✅ Complete (README.md)

**Word Count Estimate**: ~100,000+ words total across entire pack

**Files Created**: 28 files total
- 4 knowledge base files (~20,000 words)
- 4 checklists (~12,000 words)
- 1 comprehensive template (~4,000 words)
- 8 tasks (~40,000 words)
- 5 agents (~25,000 words)
- 3 workflows (~8,000 words)
- 1 README (~5,000 words)
- 1 config.yaml
- 1 building-plan.md

**Pack Status**: ✅ COMPLETE

All 7 phases finished. The BMAD Release Management expansion pack is ready for use!

**Next Steps**:
- Test pack with real release scenarios
- Gather user feedback
- Iterate based on real-world usage
- Consider additional features (CI/CD integrations, monitoring tool integrations)

---

### Session 3 - 2025-10-28 (Refactoring)
**Activities**:
- Refactored all 5 agents to match official BMAD pattern
- Removed extensive markdown documentation after YAML blocks
- Reduced agent files from ~400 lines to ~95-105 lines each
- Kept concise YAML blocks with all essential information
- Added brief "Startup Context" sections (10-20 lines) following character-psychologist pattern
- All agents now follow consistent structure:
  - BMAD Core header
  - ACTIVATION-NOTICE
  - YAML block (~80 lines)
  - Optional Startup Context (~15 lines)

**Changes Made - Agents**:
- release-manager.md: 411 lines → 99 lines (76% reduction)
- scope-analyzer.md: 392 lines → 86 lines (78% reduction)
- quality-gatekeeper.md: ~450 lines → 89 lines (80% reduction)
- deployment-coordinator.md: ~450 lines → 97 lines (78% reduction)
- communication-specialist.md: ~450 lines → 95 lines (79% reduction)

**Changes Made - Templates**:
- Rebuilt release-plan.md → release-plan.yaml to match BMAD template pattern
- Converted from markdown with {{placeholders}} and [[LLM: instructions]]
- Now uses YAML structure like story-tmpl.yaml with:
  - Template metadata (id, version, output format)
  - Workflow configuration (mode: interactive, elicitation)
  - Structured sections with id, title, type, instruction
  - Owner and editors defined per section
  - Elicit flags for interactive sections
  - Subsections for hierarchical organization
  - References to knowledge base files and checklists
  - Workflow guidance and interactive principles

**Rationale**:
Comparison with official BMAD showed:
1. Agents were too verbose - official keeps everything in YAML + minimal context
2. Templates should be YAML, not markdown - enables machine-readable structure and clear interactive flow

This refactoring makes the pack fully consistent with BMAD standards.

**Word Count After Refactoring**: ~93,000 words (down from ~100,000+)
- Agent files now contribute ~2,000 words instead of ~25,000 words
- Template converted to structured YAML (~500 lines) from markdown (~968 lines)

---

### Session 4 - 2025-10-28 (Dual-Approach Enhancement)
**Activities**:
- Enhanced Release Manager agent to support both manual and template-driven workflows
- Investigated BMAD template usage patterns by examining:
  - `.bmad-core/agents/analyst.md` (command patterns)
  - `.bmad-core/tasks/create-next-story.md` (task workflows)
  - `common/tasks/create-doc.md` (universal template processor)
- Added dual command support to release-manager.md

**Changes Made**:
- **release-manager.md**:
  - Added command: `create-plan: use task create-doc with release-plan.yaml` (template-driven)
  - Kept existing: `plan: Start manual release planning process` (guided workflow)
  - Added `create-doc.md` to task dependencies
  - Updated REQUEST-RESOLUTION with examples for both commands
  - Enhanced Startup Context to explain both approaches

**How Templates Work in BMAD**:
```
User Command → Agent → Task → Template → Output File

Example Flow:
User: *create-plan
  ↓
Release Manager (agent)
  ↓
common/tasks/create-doc.md (universal template processor)
  ↓
templates/release-plan.yaml (YAML template definition)
  ↓
docs/release/v2.1.0-release-plan.md (generated output)
```

**Two Approaches Now Available**:
1. **Manual Workflow** (`*plan`)
   - Uses `tasks/create-release-plan.md` (590 lines of step-by-step guidance)
   - Custom logic for git analysis, scope analysis, versioning decisions
   - 9-phase guided process with agent-driven interactions
   - More control and flexibility

2. **Template-Driven** (`*create-plan`)
   - Uses `common/tasks/create-doc.md` + `templates/release-plan.yaml`
   - Follows BMAD universal pattern with structured elicitation
   - Interactive section-by-section creation with 1-9 options menu
   - Consistent with other BMAD document creation workflows
   - Sections with `elicit: true` trigger mandatory user interaction

**Rationale**:
- **Manual approach**: Best for teams that need custom logic, git history analysis, and step-by-step guidance
- **Template-driven approach**: Best for teams that want consistent BMAD elicitation patterns and structured document creation
- Both approaches generate the same final document structure
- User can choose based on preference and workflow style

**Pack Status**: ✅ COMPLETE with dual-approach support

---

## Key References

- BMAD Core Architecture: `/bmad-docs/core-architecture.md`
- Expansion Pack Guide: `/docs/expansion-packs.md`
- Example Pack: `/expansion-packs/bmad-design-thinking-facilitator/`
- Example Pack: `/expansion-packs/bmad-autonomous-teams-mission-orchestra/`

---

## Open Questions / Decisions Needed

1. Should we support multiple versioning strategies (SemVer vs CalVer) or pick one?
   - **Decision**: Support both, let teams choose in pack configuration

2. How detailed should deployment steps be in the template?
   - **Decision**: TBD

3. Should we integrate with specific CI/CD tools (GitHub Actions, GitLab CI)?
   - **Decision**: Tool-agnostic, provide patterns teams can adapt

4. Should monitoring use specific tools (Datadog, New Relic)?
   - **Decision**: TBD

---

## Notes

- Keep it simple - real teams need practical, not perfect
- Focus on the 80% use case first (standard releases)
- Make it easy to customize for different team sizes and processes
- Document everything so users can adapt to their context
