---
name: test-first
description: >
  Requires proof of correctness before any implementation counts as
  done, tiered by the code's operational status. Called exclusively by
  the orchestrator skill during the implementation phase, never
  triggered on its own.
---

Determine the tier before writing code:

Tier 1 (standard) applies to exploratory, one-off, or throwaway code, the normal case for vibe coding without an existing test framework. Proof is sufficient as a before/after comparison, or a concrete example input and output showing the result matches expected behavior. No formal unit test required.

Tier 2 (escalated) applies automatically as soon as one of the following is true: the code runs, or will run, as a cron job, service, daemon, or otherwise persistent or recurring process; or the same type of bug has occurred a second time in this code or pipeline. In that case, a before/after comparison is no longer enough. Write an actual, executable test (e.g. with pytest) that fails before the implementation and passes after it. If no test infrastructure exists yet, set up a minimal one at this point (e.g. a tests/ file with pytest) instead of deferring it further.

The escalation condition "the same type of bug has occurred a second time" assumes earlier bugs are traceable, in practice usually via the change log from state-sync. If no such change log exists (e.g. because state-sync didn't fire in this session, or the project has no STATE.md yet), only what's actually visible in the current session context counts. No blind trust in an invisible history: when in doubt, treat the bug as new (Tier 1), not automatically as a repeat.

In both tiers: no "done" status without the required proof actually being delivered. Phrases like "this should work," "probably fine," or "we can test this later" are not proof and don't justify closing the task.

If you notice yourself constructing an excuse for why proof isn't needed in this particular case, treat that as a signal to provide it anyway, rather than accepting the exception.
