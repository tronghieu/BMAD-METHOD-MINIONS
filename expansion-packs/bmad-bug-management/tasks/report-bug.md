# Task: Report Bug

Agent: Bug Coordinator
Difficulty: Easy
Duration: 10–20 minutes

## Purpose
Create a high-quality bug document using the YAML template with clear reproduction steps, environment, and evidence.

## Prerequisites
- Confirm where to store: `docs/bugs/bug-<id>.md`
- If an external tracker exists, use its ID for `<id>`

## Steps
1) Create bug document using template
   - Use `templates/bug-doc-tmpl.yaml` to generate `docs/bugs/{{bug_id}}.md`
   - Ensure fields: title, severity, priority, component, reporter, created timestamp
2) Capture Steps to Reproduce (minimal but reliable)
3) Record Expected vs Actual
4) Capture Environment in table (OS/Device/AppVersion/Build/Locale)
5) Attach Evidence
   - Save files to `docs/bugs/assets/{{bug_id}}/`
   - Link artifacts under “Evidence” section
6) Initialize Links section with any known related items (PRs/commits/issue)
7) Set Status to `New`

## Checklist
- Refer to `checklists/triage-checklist.md` for completeness cues

## Outputs
- New bug document at `docs/bugs/{{bug_id}}.md`
- Assets at `docs/bugs/assets/{{bug_id}}/` (optional)

