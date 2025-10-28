# RCA Categories & Examples

Categories
- Requirements: Missing/ambiguous requirements; gap between expected and actual
- Regression: Previously working behavior broken by change
- Concurrency: Race condition, deadlock, improper synchronization
- DataShape: Schema mismatch, nullability, type/format discrepancies
- Dependency: Upstream/downstream change or version mismatch
- Design: Architectural or design flaw leading to brittleness
- Implementation: Logic bug, boundary error, incorrect assumption
- TestCoverage: Missing/insufficient tests; false sense of security

Examples
- Regression in auth after upgrading password hashing library → Dependency/Regression
- Crash on null user preference → DataShape/Implementation
- Flaky UI test due to hard waits → TestCoverage/Implementation
