# Example: Bug Lifecycle Walkthrough

Scenario: Users see a 500 error when saving profile.

1) Report
- `@bug-coordinator *report-bug`
- ID: `BUG-1234`, Title: "500 on Save Profile"
- Steps: fill minimal reproducible steps
- Evidence: attach server logs in `docs/bugs/assets/BUG-1234/`

2) Triage
- `@bug-coordinator *triage-bug`
- Severity: S1, Priority: P1 (SLA 3 days)
- Owner: assign to Dev; Component: user-profile

3) Reproduce
- `@repro-specialist *reproduce-bug`
- Minimal repro recorded; environment captured; suspected null preference in payload

4) Fix
- `@dev` → fill `Fix Plan` (failing unit test first)
- `@dev` → implement fix and `*task coverage-check`

5) Verify
- `@qa-verifier *verify-bug`
- Optionally run `@qa *review {bug}` and `@qa *gate {bug}`

6) Close
- `@bug-coordinator *close-bug`
- Link PR/commit, QA gate, and (if hotfix) release workflow
