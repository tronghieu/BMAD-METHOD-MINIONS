# Testing Levels for Bug Fixes

Guidance
- Unit: Validate fixed logic; fastest safety net
- Integration: Validate interactions across modules or services
- E2E: Validate user-visible workflows where appropriate

Recommendations
- Always add at least a unit test when possible
- Use integration tests for boundaries, I/O, or complex interactions
- Use E2E sparingly for critical paths

Targeted Regression
- Add tests for nearby risk areas identified in Fix Plan
- Prefer focused assertions over broad/unreliable checks
