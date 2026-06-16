<!-- markdownlint-disable -->

# Hardening Report: rmuir--uv-dependency-submission/v1.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **rmuir--uv-dependency-submission/v1.0.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Sub-rule (b): In the 'Submit from lockfiles' step, the run block executes `python ${ACTION_PATH}/action.py` where `ACTION_PATH` is populated from `${{ github.action_path }}` via the env block. The shell variable `${ACTION_PATH}` is unquoted, which means shell metacharacters in the value could be interpreted by the shell. It should be quoted as `"${ACTION_PATH}"` to prevent word-splitting and glob expansion. Offending line: `run: python ${ACTION_PATH}/action.py`

Locations:

- `action.yml:13`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

Quoted the ${ACTION_PATH} shell variable in the 'Submit from lockfiles' step's run block. Changed `python ${ACTION_PATH}/action.py` to `python "${ACTION_PATH}/action.py"` to prevent word-splitting and glob expansion. The ACTION_PATH value is already safely passed via the env block from ${{ github.action_path }}, so only the quoting fix was needed.

