<!-- markdownlint-disable -->

# Hardening Report: rmuir--uv-dependency-submission/v1.1.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **rmuir--uv-dependency-submission/v1.1.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Rule (b) violation: In the 'Submit from lockfiles' step, the env var ACTION_PATH (sourced from ${{ github.action_path }}, a github.* context value) is expanded unquoted in the run: shell command: `python ${ACTION_PATH}/action.py`. Any env var holding a workflow-controllable context value must be double-quoted to prevent shell metacharacter interpretation. The correct form is: `python "${ACTION_PATH}/action.py"`.

Locations:

- `action.yml:13`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

Fixed the unquoted ACTION_PATH environment variable in the 'Submit from lockfiles' step. Changed `python ${ACTION_PATH}/action.py` to `python "${ACTION_PATH}/action.py"` to prevent shell metacharacter interpretation when the github.action_path context value is expanded.

