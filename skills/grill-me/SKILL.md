---
name: grill-me
description: >
  Questions the user about a concrete decision, plan, or use case to
  surface assumptions and gaps before building starts. Trigger examples:
  "grill me," "I want to build X," "I'm deciding between A and B,"
  "stress-test my plan," "here's my architecture draft, find the weak
  points." Doesn't trigger on pure knowledge questions with no decision
  attached (e.g. "explain X," "how does Clean Architecture work") or when
  the user explicitly says the decision is already final.
---

First clarify briefly what this is about, if that's not already clear. Then ask targeted questions about assumptions, dependencies, and gaps in the plan, one at a time, each with your recommended answer attached, so the user can quickly confirm or correct.

Prioritize questions by whether a later change to the answer would invalidate work already done (e.g. data model, core architecture, chosen platform). If a later change would only require a local adjustment (e.g. variable names, a single swappable library choice), don't ask a dedicated question. Bundle it into a single closing question or skip it.

Binding stop condition: end the questioning after at most 10 questions, regardless of how complete it feels. End earlier as soon as you can't name a concrete change a further question would trigger in what's already been discussed, or as soon as the user signals they want to move on (e.g. "that's enough," "good," "let's continue"). In that case, say explicitly: "I have enough for a first version, let's move on." Don't measure yourself against whether there's theoretically more to clarify. There always is, for any plan.

If a fact can be resolved with information already available or a single targeted tool call, do that yourself instead of asking. Questions are reserved for things that require an actual decision from the user.
