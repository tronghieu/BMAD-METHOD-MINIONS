# BMAD Bug Reporting & Resolution Expansion Pack — Pack Building Proposal

This proposal defines a BMAD expansion pack that standardizes and accelerates the bug lifecycle end‑to‑end while aligning with BMAD’s story workflow, QA gates, and Release Management.

## 1) Objectives & Principles

- Standardize lifecycle: New → Assigned → In Progress → Verification (QA) → Closed, with Re‑open loop to In Progress on failed verification
- Reproducibility first: capture minimal repro, environment, and evidence
- Failing test first: write a failing test before the fix; add regression protection
- Quality gates: integrate QA verification and NFR checks before closure
- Fast path for P0/P1: hotfix variant that bridges to Release Management
- Traceability: link bug ⇄ commits/PRs ⇄ tests ⇄ releases
- Learning culture: RCA and prevention actions captured at closure

## 2) Lifecycle & Standard Process

- Detection & Reporting → New
- Triage → Assigned (or Deferred/Parked if applicable)
- Prioritization & Assignment → Owner, Severity/Priority, SLA
- Fixing → In Progress (failing test first, fix, coverage)
- Code Review → Ready for Review (part of In Progress phase)
- Verification (QA) → Verification status and quality gate
- Closure & Deployment → Closed (and linked to release/hotfix workflow)
- Re‑open loop: If verification fails, status returns to In Progress

## 3) Workflows

- Intake & Triage
  - Inputs: user report/alert/telemetry
  - Steps: validate report completeness → dedupe/link → classify (S/P/component/env) → quick repro check → assign + SLA
  - Outputs: normalized bug record, routed to owner

- Reproduction & Isolation
  - Steps: reproduce reliably → minimize repro → capture env/logs/traces → bisect/identify introducing change → record suspected root cause
  - Outputs: minimal repro asset, failing test candidate, risk notes

- Fix & Regression Protection
  - Steps: failing test first → implement fix → expand coverage (unit/integration/e2e) → NFR checks (security/perf/reliability/maintainability) → self‑review
  - Outputs: PR ready with tests, status=Ready for Review

- Verification & Gate
  - Steps: QA trace to acceptance criteria/tests → targeted regression sweep → NFR reassessment → Gate decision (PASS/CONCERNS/FAIL/WAIVED)
  - Outputs: verification evidence; FAIL loops to In Progress, PASS moves to Closure

- Closure & Release
  - Steps: document RCA → confirm backports/forward‑fixes → changelog entry → link to release/hotfix workflow → update metrics
  - Outputs: status=Closed, cross‑links created

- Hotfix Variant (P0/P1)
  - Steps: expedited triage → focused fix/tests → critical gates only → handoff to Release Management hotfix workflow → intensive monitoring → post‑mortem

## 4) Agents

- Bug Reporter: normalizes reports, elicits missing details, ensures repro quality
  - Commands: `*new-bug`, `*improve-report`, `*attach-evidence`

- Triage Master: dedupe, classify, prioritize, assign, set SLA; maintains triage board
  - Commands: `*triage`, `*dedupe`, `*assign`, `*prioritize`

- Repro Sleuth: drives minimal repro, environment capture, bisect/log analysis
  - Commands: `*repro`, `*minimize`, `*bisect`, `*collect-logs`

- Fix Engineer: enforces failing test first, fix plan, coverage, NFR checks
  - Commands: `*fix-plan`, `*write-failing-test`, `*implement-fix`, `*coverage-check`, `*cr-ready`

- QA Verifier (pairs with core QA): verification plan, traceability, targeted regression, gates
  - Commands: `*verify`, `*trace`, `*nfr`, `*gate`

- RCA Analyst: facilitates 5 Whys/FMEA, categorizes root cause, defines prevention actions
  - Commands: `*rca`, `*prevention-plan`, `*postmortem`

- Release Bridge (optional): links to standard/hotfix release workflows, comms/changelog
  - Commands: `*handoff-hotfix`, `*link-release`, `*changelog-entry`

## 5) Templates (YAML) & Checklists

- Templates (YAML, follow `bmad-core/templates` conventions)
  - bug-doc-tmpl.yaml: Full bug document generator (outputs Markdown `docs/bugs/{{bug_id}}.md`)
  - triage-notes-tmpl.yaml: Triage notes section (S/P rationale, dedupe links, ownership, SLA)
  - repro-record-tmpl.yaml: Minimal repro, env matrix, logs/traces, failing test candidate
  - fix-plan-tmpl.yaml: Hypothesis, change scope, risk areas, test plan, backport/forward‑fix
  - verification-plan-tmpl.yaml: Test matrix, targeted regression, NFR checks, gate criteria
  - rca-tmpl.yaml: 5 Whys, causal map, category, prevention actions, owners/dates
  - bug-closure-tmpl.yaml: Gate result, verification evidence, backports, release linkage

- Template conventions (YAML)
  - Include: `template.id`, `template.name`, `template.version`, `output.format`, `output.filename`
  - Use `sections` for interactive fields; keep parity with `story-tmpl.yaml` style
  - Example (abbreviated):
    ```yaml
    template:
      id: bug-doc-template-v1
      name: Bug Document
      version: 1.0
      output:
        format: markdown
        filename: docs/bugs/{{bug_id}}.md
        title: "Bug {{bug_id}}: {{title}}"
    workflow: { mode: interactive, elicitation: advanced-elicitation }
    sections:
      - id: status
        title: Status
        type: choice
        choices: [New, Assigned, InProgress, Verification, Closed]
        owner: bug-coordinator
      - id: summary
        title: Summary
        type: template-text
        template: "{{title}}"
        elicit: true
      - id: steps-to-reproduce
        title: Steps to Reproduce
        type: numbered-list
        elicit: true
      - id: expected-actual
        title: Expected vs Actual
        sections:
          - id: expected
            title: Expected
            elicit: true
          - id: actual
            title: Actual
            elicit: true
      - id: environment
        title: Environment
        type: table
        columns: [OS, Browser, Version, Build, Locale]
      - id: evidence
        title: Evidence
        instruction: "Attach links to logs/screenshots in docs/bugs/assets/{{bug_id}}/"
      - id: triage
        title: Triage Notes
        sections:
          - id: severity
            title: Severity
            type: choice
            choices: [S0, S1, S2, S3]
          - id: priority
            title: Priority
            type: choice
            choices: [P0, P1, P2, P3]
          - id: ownership
            title: Ownership
            elicit: true
      - id: verification
        title: Verification
        instruction: "Evidence and gate result; link to QA gate if used"
    ```

- Checklists (Markdown)
  - triage-checklist.md
  - reproduction-checklist.md
  - fix-checklist.md
  - verification-checklist.md
  - closure-checklist.md
  - hotfix-readiness.md

## 6) Tasks (Commands)

- Intake: `*new-bug`, `*improve-report`, `*attach-evidence`
- Triage: `*triage`, `*dedupe`, `*assign`, `*prioritize`
- Reproduction: `*repro`, `*minimize`, `*bisect`, `*collect-logs`
- Fix: `*fix-plan`, `*write-failing-test`, `*implement-fix`, `*coverage-check`, `*cr-ready`
- Verification: `*verify`, `*trace`, `*nfr`, `*gate`
- Closure: `*close-bug`, `*backport`, `*link-release`, `*changelog-entry`
- RCA & Learning: `*rca`, `*prevention-plan`, `*postmortem`
- Metrics & Hygiene: `*bug-metrics`, `*aging-review`, `*sla-audit`

## 7) Data / Knowledge Base

- Severity/Priority rubrics with SLAs
- Component taxonomy and ownership map
- Dedupe heuristics (title/stack/env similarity)
- Repro capture guide (env matrix, tools, logging levels)
- NFR quick guide for bug fixes (security/perf/reliability/maintainability)
- Testing level guidance for bug fixes (unit vs integration vs e2e)
- RCA category catalog (requirements gap, regression, concurrency, data shape, dependency)
- Commit/PR conventions for bug fixes (message format, backport tags)
- Label taxonomy: `type:bug`, `severity:*`, `priority:P*`, `area:*`, `env:*`, `cause:*`, `status:*`, `backport:*`

## 8) Integration with BMAD

- Story Flow
  - Option A: maintain standalone bug records under `docs/bugs/bug-<id>.md`, with SM/Dev/QA notes sections mirroring story files
  - Option B: convert prioritized bugs to normal BMAD stories; keep a lightweight bug stub that links to the story

- QA Gates
  - Reuse QA agent capabilities (`*trace`, `*nfr`, `*review`, `*gate`) with bug‑focused templates; output gates to `docs/qa/gates/`

- Release Management
  - P0/P1 bugs trigger the hotfix workflow; `*link-release` cross‑links bug ⇄ release and produces `*changelog-entry`

- Autonomous Teams
  - Triage routes cross‑component bugs to owning teams; include integration verification checklist for cross‑team changes

## 9) Proposed Directory Structure

- expansion-packs/bmad-bug-management/
  - agents/ (bug-reporter.md, triage-master.md, repro-sleuth.md, fix-engineer.md, qa-verifier.md, rca-analyst.md, release-bridge.md)
  - workflows/ (bug-lifecycle.yaml, hotfix-bug.yaml, backlog-hygiene.yaml)
  - tasks/ (new-bug.md, triage-bug.md, reproduce-bug.md, minimize-repro.md, bisect.md, fix-plan.md, implement-fix.md, coverage-check.md, verify-fix.md, gate-update.md, close-bug.md, rca.md, prevention-plan.md, metrics.md)
  - templates/ (bug-doc-tmpl.yaml, triage-notes-tmpl.yaml, repro-record-tmpl.yaml, fix-plan-tmpl.yaml, verification-plan-tmpl.yaml, rca-tmpl.yaml, bug-closure-tmpl.yaml)
  - checklists/ (triage-checklist.md, reproduction-checklist.md, fix-checklist.md, verification-checklist.md, closure-checklist.md, hotfix-readiness.md)
  - data/ (severity-priority-rubric.md, component-owners.md, dedupe-heuristics.md, repro-guide.md, nfr-for-bugfix.md, testing-levels.md, rca-catalog.md, commit-guidelines.md, labels.md)
  - README.md (pack overview, usage, examples)

## 10) Status Model & Transitions

- Statuses: New → Assigned → In Progress → Verification → Closed
- Re-open: Verification FAIL or regression discovered → In Progress
- Transitions performed by tasks update bug record header fields (status, owner, S/P, links)

## 11) Artifacts & Outputs

- Bug records: `docs/bugs/bug-<id>.md`
- Repro assets: `docs/bugs/assets/bug-<id>/`
- QA gates: `docs/qa/gates/`
- RCA docs: `docs/bugs/rca/bug-<id>.md`
- Metrics: `docs/bugs/metrics/`

## 12) Metrics (Recommended)

- Mean time to detect (MTTD), acknowledge (MTTA), resolve (MTTR)
- Reopen rate, escaped defects, hotfix frequency
- SLA adherence by severity/priority
- Coverage added per bug (unit/integration/e2e)

## 13) Phased Implementation Plan (when ready)

- Phase 1: Agents (Bug Reporter, Triage Master, Fix Engineer, QA Verifier), core tasks, templates, checklists
- Phase 2: Repro Sleuth, RCA Analyst, Release Bridge, data/KB
- Phase 3: Workflows (bug-lifecycle, hotfix-bug), metrics tasks, docs & examples
- Phase 4: Integrations (Release pack, Autonomous Teams), refinements from usage

## 14) Open Questions

- Prefer standalone “bug story” files vs auto‑conversion to standard stories for P1+?
- Required fields and SLAs per severity for your org?
- Default test level expectations for bug fixes (minimum unit + targeted integration)?
