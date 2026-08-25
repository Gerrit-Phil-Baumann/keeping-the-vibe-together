---
name: git-hygiene
description: >
  Checks, for non-trivial changes to existing code, whether the affected
  directory is under git version control, and replaces manual backup
  copies (.bak etc.) with commits. Called exclusively by the orchestrator
  skill, never triggered on its own.
---

Trivial (no step here needed): see the binding trivial definition in orchestrator. When in doubt, treat a case as non-trivial.

## Before the change

For a non-trivial change to an existing file: check whether the directory (or a parent directory) is a git repository.

- No git repo present: stop before making the change. Suggest `git init` plus an initial commit of the current state. Only continue after approval or explicit refusal.
- Git repo present, but in an unclean state (uncommitted or untracked changes unrelated to the current task): name this briefly, don't auto-commit it. Keep working, but don't stay silent about it.

If a safeguard before the change would make sense: suggest `git commit` (if the current state is finished) or `git stash` (if experimenting). Don't create or suggest a manual copy of the file (e.g. `file.bak`, `file.bak_20260616`, `file_old.py`). If the user proposes such a copy themselves, point them to the git alternative in a friendly way instead of silently going along with it.

## After the change

A non-trivial change only counts as complete once it's committed (or the user explicitly says not to commit right now). Don't batch multiple changes into a later commit "sometime". Commit directly after finishing the change in question, mirroring the change-log principle from state-sync.

## At session start in a project directory

Once per session, when working in a directory: a brief check for existing `.bak`, `.bak_*`, `_old`, `_backup` files and for uncommitted leftovers. If found, mention it once (don't repeat on every following request in the same session), but don't auto-clean without confirmation.

## Redundant directories

If two directories appear to cover the same code or function (e.g. an "old" and an "active" copy), name both explicitly and ask which one is canonical before continuing to work in either.

## If the user declines

If the user explicitly says to skip a step here (e.g. "no commit now," "no git init"), accept that and don't suggest it again in the same session.
