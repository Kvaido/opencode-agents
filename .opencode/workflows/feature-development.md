---
id: feature-dev
name: Feature Development
priority_order:
  - architect (if needed)
  - planner
  - coder
  - reviewer
  - tester
  - security
  - docs (always at end)
---

Standard workflow for new features.
Orchestrator invokes in order (or parallel for independent steps).
docs — final step.

## When Architect is Needed

Architect step is REQUIRED when:
- New feature changes module boundaries or adds new modules
- New feature introduces new dependencies
- Feature affects multiple modules or cross-cutting concerns
- Technical approach is unclear and needs evaluation

Architect is NOT needed when:
- Simple bug fix or small tweak
- Change is isolated to a single module
- Implementation approach is obvious and low-risk
- Only documentation or test changes

## Expected Output per Stage

| Stage | Agent | Must produce | Orchestrator verifies |
|-------|-------|-------------|----------------------|
| 1 | Architect | Architectural decisions in DECISIONS.md | DECISIONS.md was updated |
| 2 | Planner | Plan summary in RUN_CONTEXT.md | RUN_CONTEXT.md was updated |
| 3 | Coder | Implemented code + CODER_DECISIONS.md | Code changes + decision log |
| 4 | Reviewer | APPROVE or REQUEST_CHANGES verdict | Verdict is clear |
| 5 | Tester | All tests passing + coverage report | No failing tests |
| 6 | Security | No vulnerabilities (or list of issues) | Security assessment complete |
| 7 | Docs | Documentation updated + CHANGELOG.md | Docs are complete |

## Parallel Execution

Some stages can run in parallel when independent:
- reviewer + security (after coder, before tester) — ONLY if reviewer has APPROVED the code with no changes requested. If reviewer requests changes, security must wait until coder fixes and reviewer re-approves.
- Never skip stages even if running in parallel
