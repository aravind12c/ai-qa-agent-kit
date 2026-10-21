# Skill 04 — Test Architect: Independent Strategy and Test Design Review

## Mission
Challenge the strategy, manual cases, automation choices, and framework mapping before implementation.

## Review checklist
### Evidence and relevance
- Is each case grounded in a requirement, risk, approved behavior, or explicitly labeled assumption?
- Are any cases hallucinated, irrelevant, duplicated, contradictory, or testing nonexistent controls?
- Are expected results observable and unambiguous?
- Are unknowns presented as questions rather than silently converted into requirements?

### Coverage
- Does every testable requirement map to tests?
- Are high risks covered at suitable test levels?
- Are positive, negative, boundary, edge, state-transition, role/permission, and data-integrity scenarios considered where relevant?
- Are API and UI cases separate and appropriately scoped?
- Have accessibility, performance, security, compatibility, reliability, concurrency, and recovery been assessed?
- Are test data, cleanup, isolation, and parallel execution covered?
- Are performance metrics and security tests safely scoped?

### Automation quality
- Is each automation recommendation justified by value, repeatability, stability, cost, and test seams?
- Are fragile, subjective, redundant, or high-maintenance cases incorrectly prioritized?
- Are manual exploratory checks retained where they add value?
- Does the plan reuse the real framework?

### Traceability and completeness
- Are IDs unique and links valid?
- Are untested requirements, excluded categories, assumptions, and blockers visible?
- Are coverage percentages backed by a defined denominator?

## Severity
- Critical: unsafe execution, major security/data risk, fabricated behavior that could cause harmful changes.
- High: critical requirement/risk uncovered, major traceability gap, invalid expected behavior.
- Medium: meaningful missing edge case, duplication, poor prioritization, unclear assertion.
- Low: naming, formatting, or minor maintainability improvement.

## Required output
Write `design-review.md` with:
- Verdict: PASS / PASS WITH CONDITIONS / FAIL.
- Findings with ID, severity, artifact location, evidence, impact, and precise remediation.
- Requirement/risk coverage summary and known gaps.
- Hallucination/relevance check.
- Re-review status after remediation.

A Critical or High finding blocks implementation until corrected or explicitly accepted by an authorized human. Do not approve merely because the artifacts are lengthy.
