# Changelog

All notable changes to BMAD Method Minions expansion packs will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.3.0] - 2025-10-28

### Added - Release Management Expansion Pack

- **New Expansion Pack: BMAD Release Management** (28 files, ~93,000 words)
  - Comprehensive AI-powered framework for managing software releases following Agile methodologies
  - Transforms releases from stressful chaos to predictable excellence
  - Pack version: 1.0.0

- **5 Specialized Agents** (with Vietnamese historical names):
  - **Release Manager (Trần Hưng Đạo)**: Primary orchestrator for entire release lifecycle
    - Commands: `*plan`, `*create-plan`, `*monitor`, `*retrospective`, `*status`, `*workflow`
    - Dual-approach support: Manual guided workflow + Template-driven workflow
  - **Scope Analyzer (Nguyễn Trãi)**: Strategic scope analysis and inclusion/deferral recommendations
    - Commands: `*analyze`, `*recommend`, `*status`
  - **Quality Gatekeeper (Lý Thường Kiệt)**: Quality gate validation across all dimensions
    - Commands: `*validate`, `*report`, `*status`
  - **Deployment Coordinator (Võ Nguyên Giáp)**: Deployment planning and execution
    - Commands: `*plan`, `*execute`, `*rollback`, `*status`
  - **Communication Specialist (Phan Bội Châu)**: Release communications for diverse audiences
    - Commands: `*draft`, `*review`, `*template`

- **3 Release Workflows**:
  - `standard-release.yaml`: Regular releases (3-5 days, 6 phases)
  - `hotfix-release.yaml`: Emergency fixes (2-8 hours, 6 phases)
  - `major-release.yaml`: Breaking changes (4-12 weeks, 8 phases)

- **1 Comprehensive Template**:
  - `release-plan.yaml`: Interactive YAML template with 11 sections, 40+ subsections
  - Supports both manual and template-driven document creation
  - Structured elicitation with owner/editor permissions

- **8 Comprehensive Tasks** (3,000-5,000 words each):
  - `create-release-plan.md`: 9-phase manual workflow with git analysis and scope analysis
  - `analyze-scope.md`: Systematic scope analysis with recommendations
  - `run-quality-gates.md`: Comprehensive quality validation
  - `plan-deployment.md`: Deployment strategy selection and planning
  - `execute-deployment.md`: Step-by-step deployment execution
  - `monitor-release.md`: 24-48 hour post-deployment monitoring
  - `conduct-retrospective.md`: Structured learning and continuous improvement
  - `rollback-release.md`: Emergency rollback procedures

- **4 Validation Checklists**:
  - `pre-release-checklist.md`: Quality gates validation
  - `deployment-checklist.md`: Deployment execution steps
  - `post-deployment-checklist.md`: 24-48 hour verification
  - `rollback-checklist.md`: Emergency rollback decision tree

- **4 Knowledge Base Files**:
  - `release-management-kb.md`: Philosophy, principles, release types, best practices
  - `versioning-strategies.md`: SemVer, CalVer guidance with decision trees
  - `changelog-conventions.md`: Keep a Changelog, Conventional Commits standards
  - `deployment-patterns.md`: Blue-Green, Canary, Rolling, Feature Flags, Recreate patterns

- **Key Features**:
  - Support for SemVer and CalVer versioning strategies
  - Multiple deployment patterns (Blue-Green, Canary, Rolling, Feature Flags, Recreate)
  - Comprehensive quality gates (testing, security, performance, documentation, compliance)
  - Emergency rollback procedures with decision criteria
  - Post-release monitoring and retrospectives
  - Tool-agnostic approach (works with any CI/CD, monitoring tools)
  - Dual-approach: Manual workflow (*plan) + Template-driven workflow (*create-plan)

### Changed

- **Main README.md**:
  - Updated from 2 to 3 expansion packs
  - Added Release Management to expansion packs list with description and use cases
  - Added 3 real-world use cases for Release Management:
    - Standard Sprint Release
    - Emergency Hotfix
    - Major Version with Breaking Changes
  - Updated installation instructions to include Release Management pack

### Documentation

- Comprehensive `README.md` with quick start, workflows, agent descriptions, examples, best practices
- `building-plan.md`: 4-session build log documenting architecture decisions and refactoring
- `config.yaml`: Pack metadata and configuration

## [1.2.0] - 2025-10-18

### Added - Autonomous Teams Mission Orchestra v2.0.0

- **Mission PM Agent (Dao)**: Strategic mission orchestrator for cross-team product initiatives
  - `create-mission-prd`: Create cross-team mission PRD
  - `facilitate-alignment`: Run team alignment ceremony
  - `define-raci`: Create RACI matrix
  - `orchestrate-mission`: Execute full mission workflow
  - `create-team-prd`: Create team-specific PRD from handoff document

- **Mission PO Agent (Kiet)**: Mission decomposer who breaks complex initiatives into team-specific work
  - `shard-mission-to-teams`: Decompose mission PRD by team
  - `route-work`: Route work item to appropriate team or process
  - `create-team-handoff`: Generate team-specific handoff document

- **New Tasks**:
  - `create-raci-matrix.md`: Create RACI (Responsible, Accountable, Consulted, Informed) matrices for mission clarity
  - `create-team-prd-from-handoff.md`: Transform team handoffs into focused team-specific PRDs

### Changed

- **Autonomous Teams Mission Orchestra**: Updated from v1.1.0 to v2.0.0 (pack version, project v1.2.0)
  - Enhanced from 3 to 5 orchestration agents
  - Updated README with complete workflow documentation
  - Simplified agent commands to focus on essential, existing tasks
  - Updated installation instructions with correct directory naming

- **Main README.md**:
  - Fixed expansion pack directory references to use `bmad-` prefix
  - Updated installation commands with correct folder names
  - Changed installer selections to use display names

### Breaking Changes

- Mission workflow now includes Step 5: Create Team PRDs (between decomposition and team execution)
- Team PRDs now created by `mission-pm` instead of core `pm` agent
- Document structure updated: Team PRDs now live in `docs/teams/{team-id}/prd-{mission}.md`

## [1.1.0] - 2025-10-13

### Changed

#### Expansion Pack Naming Standardization

- **BREAKING**: Renamed all expansion packs to follow `bmad-` prefix convention
  - `design-thinking-facilitator` -> `bmad-design-thinking-facilitator`
  - `autonomous-teams-mission-orchestra` -> `bmad-autonomous-teams-mission-orchestra`

- Updated all `config.yaml` files with new package names
- Maintained slash prefixes for Claude Code commands:
  - Design Thinking: `bmad-dt`
  - Mission Orchestra: `bmad-atmo`

#### Version Updates

- `bmad-design-thinking-facilitator`: 1.0.0 -> 1.1.0
- `bmad-autonomous-teams-mission-orchestra`: 1.0.0 -> 1.1.0

### Added

- Updated `.gitignore` to include `node_modules`

### Fixed

- Ensured proper BMad installer detection with `.bmad-*` glob matching
- Improved IDE integration and Claude Code command support

## [1.0.0] - 2025-10-11

### Added

- **Comprehensive Repository README**: Complete introduction with:
  - About BMAD and Expansion Packs section
  - Detailed descriptions of both expansion packs
  - Real-world use cases and scenarios for each pack
  - Step-by-step installation instructions

## [0.3.0] - 2025-10-10

### Changed - Design Thinking Facilitator

- Standardized all agent definitions following BMAD core patterns
- Removed `artifact-manifest.md` to align with core architecture
- Improved agent activation instructions and command structure

## [0.2.0] - 2025-10-09

### Added - Design Thinking Facilitator Enhancements

- **Additional Tasks** (22 new task files):
  - Empathize: `conduct-user-interview.md`, `create-empathy-map.md`, `map-user-journey.md`, `facilitate-empathy-session.md`, `synthesize-research-findings.md`
  - Define: `craft-problem-statement.md`, `generate-hmw-questions.md`, `synthesize-insights.md`
  - Ideate: `run-brainstorm-session.md`, `cluster-and-theme-ideas.md`, `facilitate-idea-building.md`, `evaluate-and-prioritize.md`
  - Prototype: `plan-prototype-strategy.md`, `create-concept-sketches.md`, `create-paper-prototype.md`, `build-digital-mockup.md`, `document-prototype.md`
  - Test: `design-test-scenarios.md`, `recruit-test-participants.md`, `conduct-usability-test.md`, `analyze-test-results.md`, `plan-iterations.md`

- **Additional Templates** (23 new template files):
  - Research templates: `observation-protocol.yaml`, `user-interview-guide.yaml`, `persona-template.yaml`, `research-synthesis-board.yaml`
  - Problem definition: `pov-statement-builder.yaml`, `hmw-question-generator.yaml`, `root-cause-analysis.yaml`, `opportunity-map.yaml`
  - Ideation: `brainstorming-session-plan.yaml`, `idea-capture-board.yaml`, `idea-evaluation-matrix.yaml`
  - Prototyping: `prototype-planning-canvas.yaml`, `storyboard-template.yaml`, `solution-storyboard.yaml`, `concept-poster-template.yaml`, `prototype-specification.yaml`, `mvp-definition.yaml`
  - Testing: `test-protocol-template.yaml`, `testing-scenario-builder.yaml`, `observation-guide.yaml`, `feedback-collection-form.yaml`, `test-results-summary.yaml`, `iteration-learnings-template.yaml`

- **Additional Workflows** (3 new workflow files):
  - `service-design.yaml`: Service experience design and improvement
  - `process-improvement.yaml`: Internal process optimization
  - `strategy-workshop.yaml`: Strategic planning and direction setting

- **New Checklists**:
  - `assumption-mapping-checklist.md`: Validate assumptions before testing

### Changed

- Enhanced `define-success-metrics.md` task with measurement frameworks

## [0.1.0] - 2025-10-07

### Added - Design Thinking Facilitator Pack

- **6 Specialized Agents**:
  - `dt-master.md`: Design Thinking Master orchestrator
  - `empathy-researcher.md`: User research and empathy building specialist
  - `problem-definer.md`: Problem framing and definition expert
  - `ideation-coach.md`: Creative ideation facilitator
  - `prototype-builder.md`: Rapid prototyping specialist
  - `test-analyst.md`: User testing and validation expert

- **Agent Team Configuration**:
  - `dt-full-team.yaml`: Complete Design Thinking team setup

- **Data Resources** (4 files):
  - `brainstorming-techniques.md`: 23 ideation techniques with facilitation guidance
  - `ideation-warmups.md`: 15 creative exercises to prime thinking
  - `creative-constraints-guide.md`: Strategic constraint application frameworks
  - `design-thinking-principles.md`: Core DT philosophy and best practices

- **Core Tasks** (5 files):
  - `run-ideation-session.md`: Complete brainstorming facilitation guide
  - `conduct-user-research.md`: Empathy phase research process
  - `define-problem-statement.md`: POV and HMW question development
  - `build-rapid-prototype.md`: Fidelity selection and building guide
  - `run-user-testing.md`: User testing protocol and analysis

- **Essential Checklists** (6 files):
  - `session-preparation-checklist.md`: Universal workshop preparation
  - `phase-transition-checklist.md`: Quality gates between DT phases
  - `phase-completion-checklist.md`: Phase exit criteria
  - `idea-evaluation-checklist.md`: Multiple selection methods
  - `prototype-fidelity-checklist.md`: Fidelity decision framework
  - `insight-quality-checklist.md`: Research insight evaluation rubric

- **Templates** (2 files):
  - `empathy-map-template.md`: User empathy mapping structure
  - `problem-statement-template.md`: Problem framing template

- **Workflows** (2 files):
  - `innovation-sprint.yaml`: 5-day Design Thinking sprint
  - `product-development.yaml`: Full product development lifecycle

- **Documentation**:
  - Comprehensive `README.md` with installation, usage, and phase guides
  - Pack `config.yaml` with metadata and configuration

### Added - Autonomous Teams Mission Orchestra Pack

- **3 Orchestration Agents**:
  - `triage-master.md`: Work routing and classification
  - `mission-orchestrator.md`: Cross-team coordination
  - `integration-specialist.md`: API contract design

- **Tasks** (4 files):
  - `facilitate-alignment.md`: Team alignment ceremony
  - `orchestrate-mission.md`: Full mission orchestration workflow
  - `route-work-item.md`: Work item routing logic
  - `shard-to-teams.md`: Mission decomposition by team

- **Templates** (3 files):
  - `mission-prd-tmpl.yaml`: Cross-team mission PRD structure
  - `team-handoff-tmpl.yaml`: Team handoff document template
  - `alignment-meeting-tmpl.yaml`: Alignment meeting structure

- **Data Resources**:
  - `orchestra-config.yaml`: Team and integration configuration

- **Workflows** (2 files):
  - `mission-planning.yaml`: Mission planning process
  - `triage-routing.yaml`: Work item routing workflow

- **Documentation**:
  - Comprehensive `README.md` with workflows and use cases
  - Pack `config.yaml` with metadata

### Added - Repository Infrastructure

- **Documentation**:
  - `docs/expansion-packs.md`: Complete expansion pack creation guide
  - `docs/design-thinking-framework.md`: Design Thinking overview
  - `docs/GUIDING-PRINCIPLES.md`: Project philosophy and principles

- **Configuration**:
  - `.gitignore`: Initial ignore patterns
  - Repository structure and organization

## [0.0.1] - 2025-10-06

### Added

- Initial repository setup
- Project structure foundation
- License and basic documentation

---

## Version Naming Convention

- **Major version** (X.0.0): Breaking changes, major new features, architectural changes
- **Minor version** (0.X.0): New features, new agents, new workflows (backwards compatible)
- **Patch version** (0.0.X): Bug fixes, documentation updates, minor improvements

## Links

- [BMAD-METHOD Repository](https://github.com/bmad-code-org/BMAD-METHOD)
- [Report Issues](https://github.com/bmadcode/bmad-method/issues)
- [Discord Community](https://discord.gg/gk8jAdXWmj)

[Unreleased]: https://github.com/tronghieu/BMAD-METHOD-MINIONS/compare/v1.3.0...HEAD
[1.3.0]: https://github.com/tronghieu/BMAD-METHOD-MINIONS/compare/v1.2.0...v1.3.0
[1.2.0]: https://github.com/tronghieu/BMAD-METHOD-MINIONS/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/tronghieu/BMAD-METHOD-MINIONS/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/tronghieu/BMAD-METHOD-MINIONS/compare/v0.3.0...v1.0.0
[0.3.0]: https://github.com/tronghieu/BMAD-METHOD-MINIONS/compare/v0.2.0...v0.3.0
[0.2.0]: https://github.com/tronghieu/BMAD-METHOD-MINIONS/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/tronghieu/BMAD-METHOD-MINIONS/compare/v0.0.1...v0.1.0
[0.0.1]: https://github.com/tronghieu/BMAD-METHOD-MINIONS/releases/tag/v0.0.1
