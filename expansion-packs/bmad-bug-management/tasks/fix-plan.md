# Task: Fix Plan (Dev)

Agent: Dev (reuse core)
Difficulty: Medium
Duration: 15–30 minutes

## Purpose
Define a targeted fix approach with failing tests first, scoped changes, and risk awareness.

## Prerequisites
- Reproduction established; bug doc updated

## Steps
1) Draft Fix Plan in bug doc
   - Use `templates/fix-plan-tmpl.yaml`
   - Include hypothesis, scope (files/modules), tests to write (unit/integration/e2e), risk areas, backport/forward-fix
2) Confirm failing test first
   - Start by writing a failing test that reproduces the issue
3) Align on scope
   - Keep changes minimal; avoid opportunistic refactors

## Checklist
- Run `checklists/fix-checklist.md` during implementation

## Outputs
- Fix Plan populated in `docs/bugs/{{bug_id}}.md`

