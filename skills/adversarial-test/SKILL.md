---
name: adversarial-test
description: >
  Checks a correctness proof already delivered (from test-first) for
  whether it holds up outside the conditions under which it was produced.
  Called exclusively by the orchestrator skill, after an implementation is
  complete, before it counts as genuinely finished.
---

This skill only engages after a proof per test-first has already been delivered. It doesn't check whether something was proven, but whether the proof itself is actually meaningful.

Construct at least one input or condition the implementation was visibly not designed for: a malformed format, an empty or extremely large input, an edge case outside the originally discussed scope. Run it, mentally or actually, against the implementation, and describe concretely what would happen, rather than generally asserting it will probably work.

Additionally, formulate 1-2 verification questions about the preceding implementation's own result and answer them independently, without falling back on the original argument that led to that result. In particular, check whether prior agreement rested more on the user's framing than on independent scrutiny.

If a real problem becomes visible in the process, name it directly and concretely, even if that means the implementation no longer counts as finished. Don't soften a found problem just because that formally reopens the task.

Stop condition: one pass per completed implementation is sufficient. This skill doesn't get reapplied just because the previous check found nothing.

**Known limitation:** This skill still runs inside the same context window and with the same model that produced the original proof — it doesn't deliver a check that's fully independent of the reasoning that may have produced the error in the first place. Olausson et al. (ICLR 2024) found that GPT-4's own feedback on its own faulty code was wrong in 32 of 80 cases, against 7 of 80 for a human reviewer. At the same time, the opposite failure is just as real: an overly aggressive critic doesn't automatically help either. Vasudev, Russak, Bikel and Alshikh (2026) found that a critic model with excellent offline accuracy (AUROC 0.94) caused a 26-percentage-point performance collapse in one live agent system, by intervening in trajectories that would have succeeded on their own. Accurate skepticism isn't automatically safe skepticism. The one-pass stop condition above is a partial answer to the second problem, not a full one to the first — both limits are worth holding at once, not resolved into false comfort in either direction.
