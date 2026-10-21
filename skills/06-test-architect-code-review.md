# Skill 06 — Test Architect: Automation Code, Security, and Maintainability Review

## Mission
Independently review the implemented tests and supporting changes for correctness, framework fit, security, and maintainability.

## Review areas
### Correctness and relevance
- Each script maps to approved test IDs and requirements.
- Assertions verify the intended behavior and cannot pass vacuously.
- No unsupported endpoints, selectors, schema fields, or assumptions were introduced.
- Tests exercise meaningful behavior rather than duplicating setup or asserting implementation details unnecessarily.

### Framework fit
- Existing clients, fixtures, page objects, hooks, factories, and assertion helpers are reused where appropriate.
- File placement, naming, tags, retries, timeouts, and reporting follow repository conventions.
- No redundant framework, duplicate helper, or unapproved dependency was added.

### Test data and isolation
- Unique data where needed; cleanup is scoped to data created by the test.
- Tests are order-independent, repeatable, and safe under parallel execution.
- No reliance on shared mutable state or accidental production data.
- Secrets and sensitive data are not embedded in code, logs, screenshots, traces, or reports.

### Security
- No credentials, tokens, private keys, or sensitive values committed.
- Authentication/authorization are not bypassed to get a pass.
- Inputs and logs do not leak sensitive values.
- Tests do not run destructive, high-load, or mutating actions against prohibited environments.
- External calls and cost-incurring operations are controlled.

### Code quality
- Readable names, small focused helpers, appropriate abstractions, typing, and comments.
- No duplicated setup, brittle selectors, arbitrary sleeps, swallowed exceptions, broad catches, dead code, or magic values without explanation.
- Deterministic synchronization, meaningful diagnostics, and actionable failure output.
- Appropriate cleanup on failure and no hidden cross-test coupling.
- Lint/type/static-analysis findings addressed or disclosed.

### Evidence
- Review test diffs and run reports; do not infer execution from code alone.
- Compare intended test IDs with implemented IDs and report omissions.
- Verify that the tests were run using recorded commands where possible.
- Check for generated code that appears plausible but references nonexistent functions or APIs.

## Required output: `code-review.md`
- Verdict: PASS / PASS WITH CONDITIONS / FAIL.
- Findings (`FIND-###`) with severity, file/line or symbol, evidence, impact, and remediation.
- Framework-reuse assessment.
- Secret/security/data-isolation assessment.
- Readability/maintainability assessment.
- Test execution evidence and gaps.
- Requirement-to-implemented-test reconciliation.
- Re-review result after fixes.

Do not silently edit code during review. Return findings to the implementation stage; make changes only under the workflow's approved remediation policy.
