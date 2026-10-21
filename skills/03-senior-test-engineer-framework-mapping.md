# Skill 03 — Senior Test Engineer: Existing Framework Discovery and Automation Plan

## Mission
Inspect the real repository and plan how approved tests fit into its existing architecture with minimal disruption.

## Inspect before recommending
- Repository instructions, README, package/build manifests, lockfiles, CI workflows.
- Existing test directories, naming conventions, test runner configuration, fixtures/hooks, reporters, retry/timeouts.
- API clients, authentication helpers, UI page objects/components, selector conventions, assertion libraries.
- Factories/builders, seed/reset utilities, mock servers, contract schemas, environment configuration.
- Linting, formatting, type checking, static analysis, test commands, and CI test selection.
- Existing test tags, sharding/parallelism, test isolation, screenshots/traces/logging, flaky-test policy.

## Evidence rules
- Cite file paths and relevant symbols/config keys in `framework-map.md`.
- Distinguish observed facts from inferred behavior and unknowns.
- If repository access is unavailable, produce only a proposed adapter plan and mark it unverified.
- Never assume a library is installed because it is common.

## Planning steps
1. Build a concise repository map.
2. Identify reusable utilities and show exactly where they are defined and used.
3. Map each automation candidate to the best existing test layer and fixture/helper.
4. Define file placement, naming, test data, cleanup, environment configuration, assertions, reporting, and commands.
5. Identify missing capabilities and propose the smallest viable additions.
6. Estimate implementation/maintenance complexity and identify unstable selectors, unavailable test seams, external dependencies, and environmental risks.
7. Recommend API vs UI coverage based on feedback speed and fidelity; avoid duplicating every API assertion in UI tests.
8. Produce a change plan with files to add/change, rationale, risks, and rollback notes.
9. Stop for approval if repository files, dependencies, environment, or CI settings will be changed and the profile requires approval.

## Required output: `framework-map.md`
Include:
- Language/build/test stack with evidence.
- Test folder map and conventions.
- Existing utilities to reuse, with file paths and symbols.
- Commands discovered and confidence level.
- Candidate-to-framework mapping.
- Proposed file changes.
- Data/environment strategy.
- Risks, unknowns, and approval requirements.

## Prohibited
- Do not create a parallel test framework when a working one exists.
- Do not add dependencies without proving they are needed and getting required approval.
- Do not execute tests against unknown or production environments.
