<!-- markdownlint-disable -->

# Hardening Report: rmuir--uv-dependency-submission/v1.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **rmuir--uv-dependency-submission/v1.0.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Rule (b) violation: In the 'Submit from lockfiles' step of action.yml, the shell variable `${ACTION_PATH}` is expanded **unquoted** inside the `run:` command (`python ${ACTION_PATH}/action.py`). The variable is sourced from `${{ github.action_path }}` (a workflow-controllable context), so an attacker who controls the calling workflow could inject shell metacharacters. The fix is to double-quote the expansion: `python "${ACTION_PATH}/action.py"`.

Locations:

- `action.yml:12`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

Fixed unquoted variable expansion in action.yml line 12: changed `python ${ACTION_PATH}/action.py` to `python "${ACTION_PATH}/action.py"`. The ACTION_PATH variable is sourced from `${{ github.action_path }}` and was expanded unquoted, allowing potential shell metacharacter injection. Double-quoting the expansion prevents this.

