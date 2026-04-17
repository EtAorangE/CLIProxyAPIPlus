---
name: add-or-update-model-in-registry
description: Workflow command scaffold for add-or-update-model-in-registry in CLIProxyAPIPlus.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /add-or-update-model-in-registry

Use this workflow when working on **add-or-update-model-in-registry** in `CLIProxyAPIPlus`.

## Goal

Adds a new model or updates model routing/compatibility in the registry, often for Copilot or Gemini, including updating tests and endpoint routing logic.

## Common Files

- `internal/registry/model_definitions.go`
- `internal/registry/model_definitions_test.go`
- `sdk/api/handlers/openai/endpoint_compat.go`
- `sdk/api/handlers/openai/endpoint_compat_test.go`
- `internal/runtime/executor/github_copilot_executor.go`
- `internal/runtime/executor/github_copilot_executor_test.go`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Edit internal/registry/model_definitions.go to add or update model definition.
- Update or add tests in internal/registry/model_definitions_test.go.
- If endpoint routing is affected, update sdk/api/handlers/openai/endpoint_compat.go.
- Update or add tests in sdk/api/handlers/openai/endpoint_compat_test.go.
- If executor logic is affected, update internal/runtime/executor/github_copilot_executor.go and its tests.

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.