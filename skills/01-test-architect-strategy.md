# Skill 01 — Test Architect: Requirement Analysis and Strategy

## Mission
Convert the requirement into a risk-based, testable strategy before individual cases or scripts are created.

## Instructions
1. Read the requirement, acceptance criteria, linked design/API contracts, and relevant repository documentation.
2. Separate facts from assumptions and unknowns. Ask for clarification when uncertainty changes expected behavior, security, data integrity, scope, or release risk.
3. Break the requirement into uniquely identified, atomic requirements (`REQ-###`). Include functional and non-functional requirements.
4. Identify actors, permissions, state transitions, dependencies, integrations, data entities, error paths, and backward-compatibility concerns.
5. Perform risk analysis. Use likelihood × impact (1–5) unless the project profile specifies another model. Explain the score, not just the number.
6. Define in-scope and out-of-scope behavior, test levels, environments, test data, entry/exit criteria, regression scope, and release risks.
7. Assess these test categories as Applicable / Not applicable (with reason) / Unknown:
   - Unit/component, integration, contract, API, UI/end-to-end
   - Positive, negative, boundary, edge, state-transition, equivalence partitioning
   - Authentication, authorization, privacy, security, input validation
   - Accessibility (relevant standard/level if known), usability where required
   - Performance/load/stress/soak/scalability (only if requirements and safe environment support them)
   - Reliability/recovery, concurrency/race conditions, idempotency
   - Compatibility/browser/device/locale/time zone, data migration/integrity
   - Observability/logging, resilience/dependency failure
8. Choose test levels by feedback speed, confidence, and cost. Avoid pushing every scenario into end-to-end tests.
9. Define measurable coverage goals appropriate to the feature: requirement coverage, risk coverage, decision/branch coverage if measurable, API status/schema coverage, role/permission matrix, UI journey coverage, and non-functional acceptance thresholds when provided.
10. Define test data lifecycle, isolation, cleanup, parallelism, retries, flake policy, and evidence/reporting needs.
11. Write `requirement-intake.md` and `test-strategy.md` using templates.

## Required outputs
- Requirement inventory with acceptance criteria and traceability IDs.
- Risk register with severity, rationale, mitigation, and test implication.
- Test-type applicability matrix.
- Test strategy, scope, environments, data, entry/exit criteria, coverage targets, and open questions.
- Explicit statements of what cannot be tested yet and why.

## Prohibited
- Do not invent expected business behavior or thresholds.
- Do not claim compliance with a standard without evidence.
- Do not decide that a test type is unnecessary solely because it is expensive.
- Do not promise full coverage without a defined, measurable denominator.
