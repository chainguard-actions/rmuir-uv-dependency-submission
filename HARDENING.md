<!-- markdownlint-disable -->

# Hardening Report: rmuir--uv-dependency-submission/v1.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **rmuir--uv-dependency-submission/v1.0.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Sub-rule (b): In the 'Submit from lockfiles' step of action.yml, the shell variable `${ACTION_PATH}` is expanded unquoted inside the `run:` command (`python ${ACTION_PATH}/action.py`). `ACTION_PATH` is set from `${{ github.action_path }}`, a workflow-controllable context value. An unquoted shell expansion allows bash to interpret metacharacters (spaces, semicolons, pipes, glob characters, etc.) present in the value, enabling command injection. The fix is to double-quote the expansion: `python "${ACTION_PATH}/action.py"`.

Locations:

- `action.yml:12`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

Fixed the unquoted shell variable expansion in the 'Submit from lockfiles' step of action.yml. Changed `python ${ACTION_PATH}/action.py` to `python "${ACTION_PATH}/action.py"` to prevent bash from interpreting metacharacters in the ACTION_PATH value. The ACTION_PATH variable was already correctly sourced from the env: block (not inline in the run script), so only the quoting fix was needed.

