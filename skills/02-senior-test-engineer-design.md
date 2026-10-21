# Skill 02 — Senior Test Engineer: Test Design and Automation Feasibility

## Mission
Create a complete, traceable test catalog and decide which cases are suitable for automation.

## Design method
For each requirement and risk:
1. Derive observable outcomes from approved acceptance criteria, specifications, existing behavior, or confirmed product decisions.
2. Consider happy path, invalid input, missing input, malformed input, unauthorized/forbidden access, boundary values, equivalence classes, edge cases, state transitions, repeated requests, ordering, concurrency, dependency failure, and recovery where applicable.
3. For numeric/length/date ranges, use boundary-value analysis around min/max and just-inside/just-outside values. Do not invent boundaries: source them from a spec or mark as an open question.
4. Use decision tables for combinations of conditions and roles; use pairwise testing only when full combinations are unnecessary and the risk supports it.
5. Test API and UI separately. Include API status, schema, headers, validation, authorization, idempotency, pagination/filter/sort, rate limits, and contract cases only where supported by the actual API.
6. UI cases should cover navigation, rendering, interaction, form validation, error/loading/empty states, keyboard access, focus, accessible names, and critical responsive/browser behavior where relevant.
7. Assess accessibility with automated checks plus manual keyboard/screen-reader review where needed. Do not claim automation alone proves accessibility.
8. Performance tests must have a stated workload, metric, threshold, and safe target environment. If any are missing, create a proposal/question rather than running a load test.
9. Include data integrity, cleanup, tenant/role isolation, audit/log behavior, and privacy checks where relevant.
10. De-duplicate cases and identify the unique risk or requirement each case covers.

## Every test case must contain
- Unique ID (`TC-###`)
- Requirement ID(s) and risk ID(s)
- Title and objective
- Test level/type: API, UI, integration, contract, component, accessibility, performance, security, etc.
- Preconditions and test data
- Steps or request shape
- Expected result with observable assertions
- Priority (P0–P3) and rationale
- Positive/negative/boundary/edge classification
- Automation feasibility: Yes / Partial / No / Unknown
- Automation rationale and dependencies
- Cleanup and isolation notes
- Source/evidence and assumption status

Use `templates/test-case-catalog.csv` as the schema.

## Automation feasibility rubric
Score 1–5 for:
- Risk/release value
- Repeat frequency
- Determinism/stability
- Cost to automate and maintain (reverse score)
- Availability of stable test seams, data, and environment

Recommend automation when the value and stability justify lifecycle cost. Prefer:
1. High-risk, repeatable API regression and contract checks.
2. Authorization and data-integrity checks.
3. Stable critical UI journeys.
4. Boundary/negative regression cases that are expensive to repeat manually.
5. Accessibility smoke checks, supplemented by manual evaluation.
6. Performance automation only with agreed workload/threshold and safe infrastructure.

Keep manual or exploratory when human judgment, visual nuance, rapidly changing UX, one-off investigation, or an unstable environment makes automation poor value. A case may have both automated and manual components.

## Required outputs
- `test-cases.csv`
- `automation-matrix.csv`
- `traceability-matrix.csv`
- A concise design summary with coverage counts and uncovered requirements.

## Prohibited
- No invented endpoints, selectors, schemas, roles, limits, or expected behavior.
- Do not label a case automated merely because it could theoretically be scripted.
- Do not equate number of test cases with quality or coverage.
