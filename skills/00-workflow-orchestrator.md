# Skill 00 — QA Workflow Orchestrator

## Role
Coordinate the QA workflow. Do not perform all roles as an unchecked monolith; create distinct artifacts and conduct explicit handoffs.

## Inputs
- Requirement or change request.
- Repository root and project profile.
- Permissions, environment constraints, and available tools.

## Process
1. Read `AGENTS.md`, the project profile, and artifact contracts.
2. Create a unique run folder under the configured artifact directory. Preserve earlier runs.
3. Collect requirements and repository facts. If requirement detail is missing, use the intake template and ask only high-impact questions.
4. Invoke Skill 01 to produce strategy and risks.
5. Invoke Skill 02 to create the test catalog and automation matrix.
6. Invoke Skill 03 to inspect the repository and map framework conventions. Do not edit code yet.
7. Invoke Skill 04 as an independent reviewer. If it finds a critical/high issue, return the artifact to the relevant stage and repeat review.
8. Present the implementation plan and request approval if the profile requires it.
9. Invoke Skill 05 to implement approved automation candidates, then run safe sanity checks.
10. Invoke Skill 06 for an independent implementation/code review.
11. Fix only approved test-code findings, rerun relevant checks, and record evidence.
12. Produce the final summary and list all artifacts, unresolved findings, and untested scope.

## Gate behavior
- If a gate is not approved, stop before the gated action and leave a clear pending status.
- If tools do not support approval workflows, ask the user in chat before proceeding.
- Never treat silence as approval for destructive, costly, or shared-environment operations.

## Return format
Return: `status`, `artifacts_created`, `gate_status`, `critical_findings`, `test_execution_summary`, `unresolved_questions`, `next_action`.
