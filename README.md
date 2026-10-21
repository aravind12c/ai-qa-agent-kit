# Framework-Agnostic QA Agent Kit

A reusable, AI-assisted QA workflow for turning requirements into a reviewed test strategy, comprehensive manual/API/UI test cases, automation plans, framework-aware scripts, and a final code-quality/security review.

**Designed to minimize manual work without pretending every framework is identical.** The kit is framework-agnostic at the planning layer. Before generating executable tests, the agent must inspect your repository and map the existing framework conventions rather than inventing a new architecture.

## What this package gives you

- Six role-based skills/prompts, chained into one controlled workflow.
- Requirement clarification and traceability.
- Risk-based test strategy and coverage model.
- Manual test cases with boundary-value analysis, equivalence classes, negative cases, edge cases, accessibility, performance, API, UI, integration, security, compatibility, and reliability coverage where relevant.
- Automation feasibility and prioritization.
- Existing-framework discovery and reuse rules.
- API/UI automation implementation and sanity checks.
- Independent review gates for relevance, hallucination, coverage, maintainability, data control, and secrets.
- Machine-readable artifact templates and a configurable project profile.
- A framework adapter contract so you can integrate this with a preferred agent runner or CI pipeline.

## Package layout

```text
framework-agnostic-qa-agent-kit/
├── README.md
├── AGENTS.md
├── config/
│   └── project-profile.example.yaml
├── skills/
│   ├── 00-workflow-orchestrator.md
│   ├── 01-test-architect-strategy.md
│   ├── 02-senior-test-engineer-design.md
│   ├── 03-senior-test-engineer-framework-mapping.md
│   ├── 04-test-architect-test-review.md
│   ├── 05-senior-test-engineer-implementation.md
│   └── 06-test-architect-code-review.md
├── contracts/
│   ├── artifact-contracts.md
│   └── framework-adapter-contract.md
├── templates/
│   ├── requirement-intake.md
│   ├── test-strategy.md
│   ├── test-case-catalog.csv
│   ├── automation-matrix.csv
│   ├── traceability-matrix.csv
│   ├── review-report.md
│   └── implementation-report.md
└── integration/
    └── INTEGRATION.md
```

## Quick start

1. Copy this folder into your repository, or keep it in a central prompt/agent repository.
2. Fill in `config/project-profile.example.yaml` and save it as `config/project-profile.yaml`.
3. Give your AI agent the contents of `AGENTS.md` as its top-level operating instructions.
4. Provide the agent access to the requirements and the target repository.
5. Run the workflow in `skills/00-workflow-orchestrator.md`. The orchestrator calls the skills in order and passes their artifacts forward.
6. Require approval at the gates described below. You can automate the gates later, but do not skip them initially.
7. Run the generated tests using your existing test commands; inspect the test report and implementation report.

> **Important:** Prompts do not themselves grant repository access, execute tests, or guarantee correctness. Your agent runner needs appropriate read/write/terminal permissions. Start with least privilege and require approval before destructive commands, dependency installation, environment changes, or external service calls.

## Workflow at a glance

```text
Requirements + repository
          |
          v
[1. Test Architect: strategy + risk + scope]
          |
          v
[2. Senior Test Engineer: test design + coverage]
          |
          v
[3. Senior Test Engineer: inspect framework + automation plan]
          |
          v
[4. Test Architect: independent design/coverage review]
          |  FAIL -> return findings to relevant prior stage
          v
[5. Senior Test Engineer: implement API/UI tests + sanity run]
          |
          v
[6. Test Architect: code, security, maintainability review]
          |  FAIL -> return findings to implementation stage
          v
Final artifacts + execution evidence + known gaps
```

## Required inputs

At minimum:
- A requirement, user story, feature description, acceptance criteria, or change request.
- Access to the repository for framework-aware implementation.
- The test command(s), if they cannot be safely inferred from project documentation.

If information is missing, the agent must:
1. Separate confirmed facts, assumptions, and unknowns.
2. Ask only questions that materially affect scope, expected behavior, risk, or testability.
3. If permitted to proceed, record assumptions explicitly and mark affected tests as provisional.
4. Never invent endpoints, UI elements, selectors, schema fields, product behavior, credentials, or existing helper functions.

## Outputs

The agent should create a run-specific folder such as `qa-artifacts/<feature-slug>/<run-id>/` containing:

- `requirement-intake.md`
- `test-strategy.md`
- `test-cases.csv`
- `automation-matrix.csv`
- `traceability-matrix.csv`
- `framework-map.md`
- `design-review.md`
- `implementation-report.md`
- `code-review.md`
- `execution-summary.md`

Keep generated artifacts separate from production source files. Do not overwrite existing tests or configuration without approval.

## Definition of done

A run is complete only when:

- Every testable requirement maps to one or more tests, or has a documented reason for no test.
- Each test has a unique ID, expected result, test level/type, priority, and traceability link.
- Positive, negative, boundary, edge, state-transition, and role/permission cases are considered where applicable.
- API and UI tests are separated; integration and contract tests are included when relevant.
- Accessibility, performance, security, compatibility, reliability, and data-integrity needs are considered and explicitly marked applicable/not applicable with reasons.
- Automation candidates are prioritized by risk, repeatability, stability, execution cost, and value.
- The independent reviewer checks relevance, duplicate cases, unsupported assumptions, coverage gaps, and hallucinated behavior.
- New tests follow existing project patterns and reuse verified fixtures, clients, helpers, page objects, assertions, and data builders.
- Tests are actually run when permitted; results distinguish passed, failed, skipped, blocked, and not run.
- Code review covers security, secrets, test-data cleanup, isolation, determinism, readability, maintainability, and coding standards.
- Known gaps and limitations are disclosed. Never claim coverage or execution that was not demonstrated.

## Recommended human approval gates

| Gate | Approve before |
|---|---|
| G1: Strategy | Spending effort on a large test suite or testing against shared environments |
| G2: Design review | Writing automation |
| G3: Implementation plan | Editing project files or adding dependencies |
| G4: Execution | Running tests that can mutate shared data, call external services, or incur cost |
| G5: Final review | Merging or treating results as release evidence |

For a trusted, sandboxed repository, some gates can later be configured as automatic. Preserve explicit approval for destructive actions and production/shared-environment writes.

## Integrating with any framework

The planning skills do not assume a specific language or test runner. The implementation stage must first inspect the repository and discover:
- Language, package manager, test runner, folder layout, naming conventions.
- Existing API clients, UI page objects/components, fixtures, hooks, assertions, retries, reporters.
- Test-data factories, seed/reset utilities, environment configuration, and cleanup strategy.
- Authentication setup, mock/service virtualization approach, accessibility/performance tools.
- Lint, type-check, unit-test, and CI commands.

Then it creates `framework-map.md` and proposes the smallest compatible change. See `integration/INTEGRATION.md` and `contracts/framework-adapter-contract.md`.

## Usage prompt

Start your agent with this request:

> Read `AGENTS.md`, the project profile, and all workflow skills. Analyze the supplied requirement and inspect the repository before proposing implementation. Execute the stages in order, write each artifact to the run-specific QA artifact directory, preserve traceability, and stop at approval gates. Do not invent product behavior or framework APIs. Reuse existing framework utilities where verified. If blocked, report the exact missing input and continue only with safe, clearly labeled assumptions. Finish with a concise summary of coverage, automation, execution results, risks, and unresolved gaps.

## Safety and reliability notes

- Use synthetic or approved test data; never copy production personal data into fixtures.
- Never hardcode secrets, tokens, passwords, or private keys.
- Never point destructive tests at production.
- Prefer isolated test accounts, namespaces, tenants, and disposable data.
- Do not disable TLS, authentication, authorization, or security checks to make a test pass.
- Avoid load/performance tests against shared or production systems unless explicitly authorized.
- Tests must clean up only data they created and must not broadly delete records.
- Do not auto-fix application code to make generated tests pass.
- A passing test suite is evidence for the tested scope, not proof that the product is defect-free.
