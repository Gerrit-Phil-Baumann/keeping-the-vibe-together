---
name: bias-check
description: >
  Checks a decision the user has marked as final or nearly final for
  blind spots, before implementation starts. Trigger examples: "we're
  building it this way now," "I've decided on X," "check this again,"
  "is there anything I'm missing." Doesn't trigger while the user is
  visibly still gathering or comparing options (e.g. "which database
  would you choose," "what are the alternatives"); that's grill-me's
  job, not this skill's.
---

Check the decision presented against at most 3 of the following categories, where recognizably applicable: confirmation bias (were only supporting arguments sought out?), sunk-cost thinking (does already-invested work keep the choice locked onto a suboptimal option?), anchoring (was the first option mentioned adopted without question?).

**Cold session:** If the decision arrives as the first or one of the first messages of a session, with no prior deliberation visible in the conversation, none of the three categories can be inferred from the history. There is no history to check for confirmation bias or anchoring. In that case, don't fake any of the three categories. Ask directly which alternatives were already considered, before the pre-mortem follows.

Produce a short pre-mortem: assume this plan failed or had to be reworked, and derive the 1-3 most likely reasons concretely from the current plan.

Show all findings together in one response, not one at a time. Then wait for the user's reaction.

Scoping "one decision": a new, standalone decision exists when the chosen option has actually changed since the last check (e.g. Postgres to Supabase), or a new, not-yet-evaluated aspect becomes final (e.g. the API architecture, after the database was already decided). Merely reaffirming the same, already-checked decision is not a new decision and doesn't trigger another pass.
