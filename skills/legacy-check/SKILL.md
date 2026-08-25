---
name: legacy-check
description: >
  Analyzes existing, undocumented code or existing infrastructure before
  changes are made to it. Called exclusively by the orchestrator skill,
  never triggered on its own.
---

Trivial (no analysis step needed, act directly): see the binding trivial definition in orchestrator. When in doubt whether a case is trivial, treat it as non-trivial.

For non-trivial cases: identify recognizable dependencies and assumptions embedded in the code or system (e.g. hard-coded paths, expected formats, other components that access it). Use whatever insight is reachable with already-available information and targeted tool calls (imports, references, call sites). Full understanding of every line is not the goal in large codebases.

Explicitly separate confirmed facts (visible in the code) from assumptions (plausible but unverified).

Present the dependencies found and wait for confirmation before making the change.

If two redundant or contradictory setups exist for the same thing, name both explicitly and ask which one should remain. (Scoping against git-hygiene: this concerns content or functional redundancy, two solutions to the same underlying problem, independent of directory. git-hygiene checks structural or version-control redundancy, such as an "old" and an "active" copy of the same directory at session start. Both perspectives remain, since they catch different symptoms of the same root cause, an unclear canonical source, at different points in the workflow.)
