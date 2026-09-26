<!-- markdownlint-disable -->

# Hardening Report: rmuir--uv-dependency-submission/v1.1.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **rmuir--uv-dependency-submission/v1.1.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Rule (b) violation: In the 'Submit from lockfiles' step of action.yml, the run block executes `python ${ACTION_PATH}/action.py` where `ACTION_PATH` is sourced from `${{ github.action_path }}` via the env block. The shell variable expansion `${ACTION_PATH}` is unquoted, so if the action path contained shell metacharacters (e.g. spaces, semicolons, or subshell syntax), bash would interpret them, enabling command injection. The fix is to quote the expansion: `python "${ACTION_PATH}/action.py"`.

Locations:

- `action.yml:12`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

Fixed unquoted shell variable expansion in action.yml line 12. Changed `python ${ACTION_PATH}/action.py` to `python "${ACTION_PATH}/action.py"` to prevent potential command injection if the action path contains shell metacharacters (spaces, semicolons, subshell syntax, etc.).

