# Integration Guide

## Integration pattern

Use this kit as a prompt-and-artifact layer around your preferred agent framework. Keep the role prompts stable and implement repository access, file writes, approvals, and test execution using your runner's native tools.

## Minimum integration sequence

1. **Load instructions:** provide `AGENTS.md`, project profile, and the orchestrator prompt as system/project instructions.
2. **Supply requirements:** attach the requirement, acceptance criteria, API contracts, design links, and relevant product docs.
3. **Discover repository:** grant read-only access first. Let Skill 03 inspect the project before any code is generated.
4. **Persist artifacts:** enable writes only to the run-specific QA artifact directory during planning.
5. **Review:** run the independent design review and resolve blocking findings.
6. **Approve implementation:** show the planned file diff and commands before granting write/execute permissions.
7. **Implement and execute:** allow only repository-verified commands and an explicitly approved non-production target.
8. **Review implementation:** run the code review skill, remediate approved findings, and rerun relevant checks.
9. **Publish evidence:** preserve reports, test output, traceability, and unresolved gaps as CI artifacts if desired.

## Map the adapter to your platform

Your runner needs equivalents for:
- Reading repository files and listing directories.
- Searching symbols/configuration and inspecting diffs.
- Writing files within a restricted directory.
- Running approved terminal commands.
- Capturing exit codes and output.
- Asking for human approval.
- Redacting secrets from logs.
- Passing stage outputs to the next prompt.

Do not assume all agent frameworks have the same tool names or permission model. Use `contracts/framework-adapter-contract.md` as the behavioral contract, then map it to your framework's native API.

## CI/CD recommendation

Initially run this as an assisted workflow on a branch. Once stable, automate low-risk stages:
- Requirement/test artifact validation.
- CSV schema and unique-ID checks.
- Traceability consistency checks.
- Lint/type checks and targeted tests.
- Report archiving.

Keep human approval for requirement ambiguity, new dependencies, broad code changes, production/shared-environment actions, destructive tests, and load tests unless your organization has a documented safe policy.

## Before using in a real project

- Replace example project settings.
- Add your approved environment and test-data policy.
- Define the applicable security/accessibility/performance standards.
- Verify all commands and tools against the actual repository.
- Decide who can approve gates and accept residual risks.
- Test the workflow on a small feature before scaling it.
