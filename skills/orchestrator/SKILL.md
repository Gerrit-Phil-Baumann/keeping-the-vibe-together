---
name: orchestrator
description: >
  Determines, for every new request, the order in which grill-me,
  bias-check, state-sync, legacy-check, test-first, adversarial-test, and
  git-hygiene apply. Trigger: every new user request in this project,
  before any answer or implementation begins.
---

Check, for every new request, in this order, which steps apply:

1. Is the request non-trivial (definition: see below in this file; when in doubt, non-trivial)? If yes: run state-sync first, to load project state.
2. Does the request contain a new, not-yet-decided question with real stakes (would affect what's already been discussed if the answer later changes)? If yes: run grill-me before anything gets implemented.
3. Does the user mark a decision as final or nearly final? If yes: run bias-check, once per decision, per its own scoping rule.
4. Does the implementation involve a non-trivial change to something that already exists? If yes: run legacy-check before changing anything, then git-hygiene (git state of the affected directory), before actually changing anything.
5. Is code actually being implemented or changed in this request? If yes: run test-first during implementation, then adversarial-test, then git-hygiene (commit instead of backup copy, final commit), before the implementation counts as done.
6. Is the request a pure knowledge question with no decision of the user's own attached (e.g. "explain X," even if terms like "architecture" appear in it)? If yes: none of the above steps apply, answer directly. This point is listed last but acts as a priority exception: a substantial, decision-free knowledge question overrides every other point, regardless of how non-trivial it looks on its face.

**Trivial definition (binding, single source; state-sync, legacy-check, and git-hygiene reference this instead of duplicating it):** Trivial means renaming a file, formatting, comments, typo fixes, and config values with no runtime effect (e.g. labels, cosmetic defaults). Not trivial: config values with runtime effect (timeouts, limits, feature flags, paths, credentials, even a single value), moving, restructuring, replacing, removing, and content changes to existing logic, regardless of how small the change looks locally. When in doubt, a change counts as non-trivial.

These seven skills don't reference each other and don't assume one another. Every activation runs exclusively through this order here. When adding further skills, only this file gets adjusted.

If the user explicitly wants to skip a step, accept that without further pushback, and don't repeat the point on every following request in the same session.

**Visibility line:** For every non-trivial request, briefly state which of the seven skills were actually applied (e.g. "Dispatcher: state-sync, legacy-check, test-first applied"), before the actual answer follows. Without this signal, a check that silently didn't fire is indistinguishable from a check that genuinely wasn't needed.

**Known limitation:** This stack is self-imposed discipline via prompt-following, not an externally enforced rule -- no hook, no CI gate, no technical control that physically prevents a skipped check. In a very long session, where this system context gets crowded out of the effective attention window, this check can fail to fire and nothing will announce that it didn't. That's a known, unresolved property of this approach, not a solved one. When in doubt about your own reliability in a long session, say so openly instead of staying silent about it.
