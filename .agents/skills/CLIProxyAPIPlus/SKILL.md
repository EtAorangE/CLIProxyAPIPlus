```markdown
# CLIProxyAPIPlus Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches you how to contribute to the CLIProxyAPIPlus Go codebase, which provides a programmable proxy API for various AI model providers (such as Copilot, Codex, Gemini, and Cursor). You'll learn the project's coding conventions, commit patterns, and the main workflows for adding models, fixing cache logic, updating documentation, and more. This guide is ideal for both new and experienced contributors looking to follow established practices and streamline their workflow.

## Coding Conventions

- **Language:** Go
- **Framework:** Go standard library and project-specific structure

### File Naming

- Use `snake_case` for file names.
  - Example: `model_definitions.go`, `codex_executor_cache_test.go`

### Import Style

- Use **relative imports** within the project.
  - Example:
    ```go
    import (
        "internal/registry"
        "sdk/api/handlers/openai"
    )
    ```

### Export Style

- Use **named exports** for functions, types, and variables.
  - Example:
    ```go
    // Exported function
    func NewExecutor() *Executor { ... }

    // Exported type
    type ModelDefinition struct { ... }
    ```

### Commit Patterns

- Commit types: `fix`, `feat`, `docs`, `refactor`, `chore`
- Prefix each commit message with the type.
  - Example: `fix: handle Codex cache affinity for session continuity`
- Average commit message length: ~57 characters

## Workflows

### Add or Update Model in Registry
**Trigger:** When you want to add support for a new model or fix model routing in the registry (e.g., Copilot, Gemini).
**Command:** `/add-model`

1. Edit `internal/registry/model_definitions.go` to add or update the model definition.
2. Update or add tests in `internal/registry/model_definitions_test.go`.
3. If endpoint routing is affected, update `sdk/api/handlers/openai/endpoint_compat.go`.
4. Update or add tests in `sdk/api/handlers/openai/endpoint_compat_test.go`.
5. If executor logic is affected, update `internal/runtime/executor/github_copilot_executor.go` and its tests.

**Example:**
```go
// internal/registry/model_definitions.go
var SupportedModels = map[string]ModelDefinition{
    "new-model": {
        Name: "new-model",
        Provider: "gemini",
        // ...
    },
}
```

---

### Codex Continuity or Cache Fix
**Trigger:** When you need to fix, refactor, or improve Codex prompt cache continuity or affinity handling.
**Command:** `/codex-cache-fix`

1. Edit `internal/runtime/executor/codex_continuity.go` for continuity logic.
2. Edit `internal/runtime/executor/codex_executor.go` for main executor changes.
3. Update or add tests in `internal/runtime/executor/codex_executor_cache_test.go`.
4. If websockets are affected, update `internal/runtime/executor/codex_websockets_executor.go` and its test.
5. If API handler logic is affected, update `sdk/api/handlers/handlers.go`.
6. If affinity or conductor logic is affected, update `sdk/cliproxy/auth/conductor.go` and its tests.

**Example:**
```go
// internal/runtime/executor/codex_continuity.go
func MaintainSessionAffinity(sessionID string) error {
    // logic for session continuity
}
```

---

### Add or Update README Sponsorship or Links
**Trigger:** When you want to add or update sponsorship banners, links, or formatting in README files.
**Command:** `/update-readme-sponsor`

1. Edit `README.md`, `README_CN.md`, and `README_JA.md` to update sponsorship or links.
2. If needed, add or update image assets (e.g., `assets/bmoplus.png`, `assets/lingtrue.png`).

---

### Clarify Provider-Specific Routing or Paths in Docs
**Trigger:** When you want to clarify or neutralize provider-specific routing/path wording in docs.
**Command:** `/clarify-provider-docs`

1. Edit `README.md`, `README_CN.md`, and `README_JA.md` for documentation wording.
2. Edit `config.example.yaml` if configuration examples need clarification.

---

### Cursor Provider Feature Development
**Trigger:** When you want to add or improve Cursor provider features (multi-account, session, error handling, management API).
**Command:** `/cursor-feature`

1. Edit or add files under `internal/auth/cursor/` (e.g., `filename.go`, `oauth.go`, `proto/*`).
2. Edit `internal/runtime/executor/cursor_executor.go` for executor logic.
3. Edit `internal/api/handlers/management/auth_files.go` for management API.
4. Edit `sdk/auth/cursor.go` for SDK integration.
5. Edit `internal/api/server.go` if new routes are added.
6. Edit `internal/cmd/cursor_login.go` for CLI changes.

---

### Fix or Improve Codex Executor Error Handling
**Trigger:** When you want to fix Codex executor error handling or parameter compatibility.
**Command:** `/fix-codex-error`

1. Edit `internal/runtime/executor/codex_executor.go` for error handling or parameter logic.
2. If needed, update `internal/runtime/executor/codex_executor_retry_test.go`.

**Example:**
```go
// internal/runtime/executor/codex_executor.go
func (e *CodexExecutor) Execute(req *Request) (*Response, error) {
    // Improved error handling logic
}
```

---

## Testing Patterns

- **Test File Naming:** Use the pattern `*_test.go`.
  - Example: `model_definitions_test.go`, `codex_executor_cache_test.go`
- **Testing Framework:** Not explicitly specified, but uses Go's standard `testing` package.
- **Test Placement:** Place tests in the same package as the code, in files ending with `_test.go`.
- **Example Test:**
    ```go
    // internal/registry/model_definitions_test.go
    func TestModelDefinition(t *testing.T) {
        // test logic here
    }
    ```

## Commands

| Command               | Purpose                                                                                   |
|-----------------------|-------------------------------------------------------------------------------------------|
| /add-model            | Add or update a model in the registry and update related routing/tests                    |
| /codex-cache-fix      | Fix or improve Codex prompt cache continuity, affinity, or error handling                 |
| /update-readme-sponsor| Add or update sponsorship banners, links, or formatting in README files                   |
| /clarify-provider-docs| Clarify provider-specific routing or path limitations in documentation and config examples |
| /cursor-feature       | Implement or improve Cursor provider features (multi-account, session, error handling)    |
| /fix-codex-error      | Fix or improve Codex executor error handling or parameter compatibility                   |
```
