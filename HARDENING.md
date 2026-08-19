<!-- markdownlint-disable -->

# Hardening Report: rmuir--uv-dependency-submission/v1.1.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **rmuir--uv-dependency-submission/v1.1.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Rule (b) violation in action.yml: the `run:` block expands `${ACTION_PATH}` without double-quoting it (`python ${ACTION_PATH}/action.py`). The variable `ACTION_PATH` is sourced from `${{ github.action_path }}` (a `github.*` context). An unquoted shell variable expansion allows the shell to parse metacharacters out of the value. The fix is to quote the expansion: `python "${ACTION_PATH}/action.py"`.

Locations:

- `action.yml:10`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

Fixed unquoted variable expansion in action.yml line 10: changed `python ${ACTION_PATH}/action.py` to `python "${ACTION_PATH}/action.py"`. The ACTION_PATH env var was already properly set via the step's `env:` block; only the double-quoting of the shell expansion was missing.

