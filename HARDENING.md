<!-- markdownlint-disable -->

# Hardening Report: rmuir--uv-dependency-submission/v1.1.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `374911c4be584df24e6da57af2d990570ef0f859`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **rmuir--uv-dependency-submission/v1.1.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Rule (b) violation: the env var ACTION_PATH, set from the workflow context github.action_path, is expanded without double quotes in the run block: `run: python ${ACTION_PATH}/action.py`. The shell will split it on whitespace and expand glob characters. Quote it: `python "${ACTION_PATH}/action.py"`.

Locations:

- `action.yml:13`

### prior-fix (severity: high)

Carried forward from this version's previous harden, which fixed it; fix it again unless the code no longer has the problem. The previous harden changed action.yml without recording a finding for it, and this analysis reported nothing there. Re-apply its security changes unless the code no longer needs them. The previous patch:
```diff
diff --git a/action.yml b/action.yml
index 91f15b1..2bb1037 100644
--- a/action.yml
+++ b/action.yml
@@ -1,16 +1,32 @@
 name: uv Dependency Submission
 description: Parses uv lock files and submits to the dependency graph
-
 runs:
   using: "composite"
   steps:
     - name: Setup Python
       uses: actions/setup-python@a309ff8b426b58ec0e2a45f0f869d46889d02405 # v6.2.0
       with:
         python-version: "3.12"
     - name: Submit from lockfiles
       shell: bash
-      run: python ${ACTION_PATH}/action.py
+      run: python "${ACTION_PATH}/action.py"
       env:
         ACTION_PATH: ${{ github.action_path }}
         GH_TOKEN: ${{ github.token }}

```

Locations:

- `action.yml`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, prior-fix

**Notes:**

Quoted ${ACTION_PATH} in action.yml run step: python "${ACTION_PATH}/action.py". setup-python was already pinned by SHA.

