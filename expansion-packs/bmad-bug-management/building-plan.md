# Building Plan: BMAD Bug Reporting & Resolution Pack

## Purpose
Track cross-session implementation of the Bug Management expansion pack and keep scope aligned with BMAD core and Release Management.

---

## High‑Level Architecture Decisions

### Agents (3 + reuse core Dev)
- Bug Coordinator — intake, triage, assignment, status control
- Repro Specialist — minimal repro, env/evidence, bisect/logs when needed
- QA Verifier — verification plan, targeted regression, gate update (pairs with core `qa`)
- Reuse `bmad-core/agents/dev.md` for fixing and tests (no separate Fix Engineer agent)

### Workflows (2)
- bug-lifecycle.yaml — New → Assigned → In Progress → Verification → Closed (Reopen → In Progress)
- hotfix-bug.yaml — expedited triage, focused tests, critical gates, handoff to Release Hotfix

### Templates (YAML, 7)
- bug-doc-tmpl.yaml (full bug document → `docs/bugs/{{bug_id}}.md`)
- triage-notes-tmpl.yaml
- repro-record-tmpl.yaml
- fix-plan-tmpl.yaml
- verification-plan-tmpl.yaml
- rca-tmpl.yaml
- bug-closure-tmpl.yaml

### Tasks (10)
report-bug, triage-bug, reproduce-bug, fix-plan, resolve-bug, coverage-check, verify-bug, gate-update, close-bug, rca-and-prevention

### Checklists (5)
triage-checklist.md, reproduction-checklist.md, fix-checklist.md, verification-checklist.md, closure-checklist.md

### Data / Knowledge Base (4)
severity-priority-rubric.md, repro-guide.md, testing-levels-for-bugs.md, rca-catalog.md

### Storage & Integration
- Bug files: `docs/bugs/bug-<id>.md`; evidence under `docs/bugs/assets/<id>/`
- QA gates: `docs/qa/gates/bug-<id>.yml` (reusing core `qa-gate-tmpl` semantics)
- Release linkage: Close step writes changelog entry and links to Release or Hotfix

---

## Build Order & Status

### Phase 0: Proposal ✅ COMPLETE
**Goal**: Align scope and decisions

- [x] Draft pack vision and scope
- [x] Save as `pack-building-proposal.md`

**Status**: Complete (2025-10-28)

---

### Phase 1: Foundation ✅ COMPLETE
**Goal**: Create skeleton files and metadata

- [x] Create `config.yaml` (pack metadata for installers)
- [x] Create folder structure (agents/, workflows/, tasks/, templates/, checklists/, data/, docs/)
- [x] Add `README.md` (pack overview, usage)

**Acceptance**: `bmad-method validate` passes basic structure; README lists agents, tasks, workflows
**Status**: Complete (2025-10-28)

---

### Phase 2: Templates (YAML) ✅ COMPLETE
**Goal**: Author YAML templates modeled after `bmad-core/templates/story-tmpl.yaml`

- [x] `templates/bug-doc-tmpl.yaml` (primary generator)
- [x] `templates/triage-notes-tmpl.yaml`
- [x] `templates/repro-record-tmpl.yaml`
- [x] `templates/fix-plan-tmpl.yaml`
- [x] `templates/verification-plan-tmpl.yaml`
- [x] `templates/rca-tmpl.yaml`
- [x] `templates/bug-closure-tmpl.yaml`

**Acceptance**: Each template has `template`, `output`, `sections` and renders without schema errors
**Status**: Complete (2025-10-28)

---

### Phase 3: Checklists ✅ COMPLETE
**Goal**: Codify validation steps

- [x] `checklists/triage-checklist.md`
- [x] `checklists/reproduction-checklist.md`
- [x] `checklists/fix-checklist.md`
- [x] `checklists/verification-checklist.md`
- [x] `checklists/closure-checklist.md`

**Acceptance**: Each checklist referenced by tasks; concise and actionable
**Status**: Complete (2025-10-28)

---

### Phase 4: Tasks ✅ COMPLETE
**Goal**: Define agent actions and interactive elicitation

- [x] `tasks/report-bug.md`
- [x] `tasks/triage-bug.md`
- [x] `tasks/reproduce-bug.md`
- [x] `tasks/fix-plan.md` (to be run by core Dev)
- [x] `tasks/resolve-bug.md` (failing test first → fix)
- [x] `tasks/coverage-check.md` (targeted regression)
- [x] `tasks/verify-bug.md`
- [x] `tasks/gate-update.md` (wrap core `qa *gate`)
- [x] `tasks/close-bug.md` (links, changelog, backports)
- [x] `tasks/rca-and-prevention.md`

**Acceptance**: Tasks reference templates/checklists and emit expected artifacts/fields
**Status**: Complete (2025-10-28)

---

### Phase 5: Agents ✅ COMPLETE
**Goal**: Define personas and dependencies

- [x] `agents/bug-coordinator.md`
- [x] `agents/repro-specialist.md`
- [x] `agents/qa-verifier.md`
- (Reuse core) Dev agent for fix execution

**Acceptance**: Agents load only their dependencies; startup help lists tasks
**Status**: Complete (2025-10-28)

---

### Phase 6: Workflows ✅ COMPLETE
**Goal**: End-to-end lifecycle

- [x] `workflows/bug-lifecycle.yaml`
- [x] `workflows/hotfix-bug.yaml`

**Acceptance**: Happy-path walkthrough produces all expected outputs and transitions
**Status**: Complete (2025-10-28)

---

### Phase 7: Data / KB ✅ COMPLETE
**Goal**: Lightweight guidance and rubrics

- [x] `data/severity-priority-rubric.md`
- [x] `data/repro-guide.md`
- [x] `data/testing-levels-for-bugs.md`
- [x] `data/rca-catalog.md`

**Acceptance**: Referenced by templates/tasks; pragmatic and brief
**Status**: Complete (2025-10-28)

---

### Phase 8: Integration Wiring ✅ COMPLETE
**Goal**: Connect to QA and Release

- [x] QA: verify `*verify-bug` + `*gate-update` interoperates with core `qa` outputs
- [x] Release: verify hotfix handoff (P0/P1) and changelog entry in `close-bug`

**Acceptance**: QA gate files written as expected; Release linkage present for hotfixes
**Status**: Complete (2025-10-28)

---

### Phase 9: Documentation & Examples ✅ COMPLETE
**Goal**: Usability and onboarding

- [x] Flesh out `README.md` (overview, quick start, examples)
- [x] Add `docs/examples/` with 1 sample bug flow

**Acceptance**: A new user can run the lifecycle end-to-end using docs
**Status**: Complete (2025-10-28)

---

### Phase 10: Validation & Refinement ⬜ NOT STARTED
**Goal**: Test and iterate

- [ ] Run `npx bmad-method validate` (if applicable)
- [ ] Dry-run workflows end-to-end
- [ ] Address gaps; update docs

**Acceptance**: Smooth execution across agents and tasks; no broken links

---

## Session Log

### Session 1 — 2025-10-28
**Activities**:
- Aligned on storage (`docs/bugs/bug-<id>.md`) and YAML templates
- Decided to reuse core `dev` for fixes (no Fix Engineer agent)
- Created `pack-building-proposal.md` (scope, workflows, agents, templates, tasks, data)
- Created this `building-plan.md` to track phases and tasks

**Progress**:
- Phase 0: COMPLETE
- Phases 1–10: NOT STARTED (queued)
