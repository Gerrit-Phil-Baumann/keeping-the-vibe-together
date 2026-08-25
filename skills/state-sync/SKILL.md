---
name: state-sync
description: >
  Loads and maintains two linked documents per project: a technical state
  file (STATE.md) in the code repo with a change log, and a narrative
  journal in a personal note system (e.g. Obsidian, Notion, or a plain
  markdown file), cross-referenced. Called exclusively by the orchestrator
  skill, never triggered on its own.
---

At the start of a session, look for two linked documents for the project at hand:

1. **STATE.md at the repo root**: the technical truth. Infrastructure facts, running services, architecture decisions made (with reasoning), open items, change log. For a file up to 200 lines, read it in full; for longer files, read headings and structure first and load individual sections as needed.
2. **Narrative journal** for the same project, in a personal note system (e.g. an Obsidian vault, Notion, or a plain markdown file outside the repo), in the same folder or area as existing project documentation, if any. The narrative layer: what was decided and why, what friction or mood came with it, a record over time. Shorter than STATE.md and standalone: a living piece of writing that references the corresponding STATE.md for the facts, without duplicating the technical details.

**Fallback when no note system is reachable:** If no personal note system is configured or reachable in the current environment (e.g. a sandbox or CI context without access to external tools), create the narrative journal instead as `journal.md` at the repo root, next to STATE.md. This is a substitute, not an equivalent. Mark once, inside the journal itself, that this is the fallback, so it isn't mistaken for a duplicate when later merged into a real note system.

**Public repos:** If the repo is also meant for publication, STATE.md and any `journal.md` fallback don't automatically belong in what gets published. Both are working notes, not content meant for others. Before the first commit, clarify whether both files should be tracked (part of the history, and therefore public) or kept local via `.gitignore`. When in doubt, keep them local and don't publish them by default. This applies whether the narrative journal lives in a real note system or as the in-repo fallback.

Trivial (neither document gets created or updated if none exists yet): see the binding trivial definition in orchestrator. When in doubt whether a case is trivial, treat it as non-trivial.

For non-trivial tasks with no existing STATE.md: create it at the repo root. With no existing narrative journal for the project: create one (in the note system, or via the fallback as `journal.md`, see above), referencing STATE.md.

Maintain a separate change-log section within STATE.md. Log (timestamp, what, why): every non-trivial change per the definition in orchestrator. Don't log trivial changes.

Before setting up something new, check in STATE.md whether something already exists for it. If you find two parallel solutions to the same problem, actively point that out.

Update STATE.md (facts and change log) and the narrative journal directly after finishing the change in question, not batched at the end of a session. Both documents get updated together for the same change, never just one of the two. Otherwise they drift apart.

**Known limitation:** The technical half of this file — STATE.md, the change log — is close to fact by construction: timestamped as it happens, not reconstructed afterward. The narrative half is a different animal. Research on model self-explanation (Turpin et al., 2023; Chen et al., Anthropic, 2025) has found that models asked to explain *why* they made a decision often produce something coherent, detailed, and disconnected from the actual reason — in the Anthropic study, models that had visibly used a hidden hint in a task acknowledged doing so only 25–39% of the time, filling the rest with plausible-sounding reasoning that simply wasn't what happened. A narrative journal written by the same model that made the decision inherits that risk. Not a reason to skip the journal — a reason to trust the change log over the story sitting next to it, whenever the two disagree.
