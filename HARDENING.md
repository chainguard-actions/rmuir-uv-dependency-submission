<!-- markdownlint-disable -->

# Hardening Report: rmuir--uv-dependency-submission/v1.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **rmuir--uv-dependency-submission/v1.0.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Sub-rule (b): an unquoted shell expansion of an env var that holds a github.* value (ACTION_PATH: ${{ github.action_path }}). Offending line: `run: python ${ACTION_PATH}/action.py`. Wrap it in double quotes: `python "${ACTION_PATH}/action.py"`.

Locations:

- `action.yml:12`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

Wrapped ${ACTION_PATH}/action.py in double quotes in action.yml (shell: bash).

