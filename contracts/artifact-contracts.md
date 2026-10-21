# Artifact Contracts

These contracts define the minimum content expected from each stage. The templates in `templates/` provide starter formats.

## Requirement intake
Must include:
- Requirement source and version/date if known.
- Requirement IDs and acceptance criteria.
- Confirmed facts, assumptions, unknowns, and questions.
- Actors, roles, states, integrations, data entities, constraints.
- Out-of-scope items and evidence links.

## Test strategy
Must include:
- Scope, risk register, test-level strategy, applicability matrix.
- Test environments and target safety.
- Test data lifecycle, setup, cleanup, isolation, and parallelism.
- Coverage goals with explicit denominators.
- Entry/exit criteria, regression plan, reporting, and known gaps.

## Test case CSV
Required columns:
`test_id, requirement_ids, risk_ids, title, objective, test_level, test_type, priority, classification, preconditions, test_data, steps_or_request, expected_result, automation_feasibility, automation_rationale, cleanup, source_evidence, assumption_status`

Use semicolon-separated values inside ID fields when a case maps to multiple IDs. Quote CSV fields correctly.

## Automation matrix
Required columns:
`automation_id, test_id, layer, recommendation, value_score, repeatability_score, stability_score, maintenance_cost_score, dependencies, rationale, implementation_status`

Scores are 1–5. Define score direction consistently; for maintenance cost, 5 means low cost/easy to maintain. Do not calculate a composite score unless weights are documented.

## Traceability matrix
Required columns:
`requirement_id, acceptance_criterion, risk_ids, manual_test_ids, automation_ids, coverage_status, gap_or_reason`

Coverage status is one of `COVERED`, `PARTIAL`, `NOT_COVERED`, `NOT_TESTABLE_YET`, `NOT_APPLICABLE`.

## Review reports
Must include verdict, findings with severity and evidence, coverage gaps, unsupported assumptions, remediation, and re-review status.

## Execution summary
For each command/test group, record command, target environment, timestamp if available, exit code, and counts for passed/failed/skipped/blocked/not-run. Never fabricate evidence.
