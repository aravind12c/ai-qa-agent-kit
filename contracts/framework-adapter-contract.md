# Framework Adapter Contract

The kit does not mandate a specific agent framework, test runner, programming language, or automation library. Implement this contract in your agent runner/integration layer.

## Adapter responsibilities

### 1. Repository discovery
Input: repository root and read permissions.
Output:
- File tree summary (exclude secrets, build artifacts, dependency caches).
- Language/package manifests.
- Test runner and configuration evidence.
- Existing tests, fixtures, helpers, commands, and CI conventions.
- Evidence file paths and uncertainty notes.

### 2. Artifact persistence
Input: artifact type, run ID, content.
Output:
- Writes only within the approved artifact directory.
- Never overwrites prior runs by default.
- Reports created paths and write failures.
- Validates CSV headers and IDs.

### 3. Stage execution
Input: skill prompt, required inputs, previous artifact references.
Output:
- Stage result with status: `SUCCESS`, `NEEDS_INPUT`, `BLOCKED`, or `FAILED`.
- Artifact paths.
- Findings and unresolved questions.
- Explicit assumptions.
- Evidence references.

### 4. Approval gate
Input: action and risk level.
Output: `APPROVED`, `REJECTED`, or `PENDING`.
Require explicit approval for writes, dependency installs, shared-environment mutation, destructive actions, load tests, and external cost-incurring calls according to project policy.

### 5. Test execution
Input: repository-verified command and approved target environment.
Output:
- Exact command and exit code.
- stdout/stderr summary with secrets redacted.
- Test counts and report paths.
- Environment and timestamp if available.
- Never infer success from absence of output.

### 6. Secret handling
- Use a secret manager or injected environment variables.
- Redact secrets before storing logs.
- Do not print environment variables wholesale.
- Do not scan or expose unrelated private files.

## Suggested stage interface

```json
{
  "stage": "test-design",
  "run_id": "feature-2026-10-21-001",
  "inputs": [
    "requirement-intake.md",
    "test-strategy.md"
  ],
  "outputs": [
    "test-cases.csv",
    "automation-matrix.csv",
    "traceability-matrix.csv"
  ],
  "status": "SUCCESS",
  "assumptions": [],
  "blockers": [],
  "evidence": []
}
```

This is an illustrative contract, not a claim that every agent runner accepts this schema. Map it to the runner's native tool/action format.
