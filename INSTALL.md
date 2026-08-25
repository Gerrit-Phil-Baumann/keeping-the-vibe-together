# Installing the Discipline Stack

These are Claude Skills: markdown files with a short YAML frontmatter (`name`, `description`) plus plain-language instructions. Any environment that supports Claude Skills can load them.

## Claude Projects (claude.ai)

1. Create a new Project.
2. Upload all eight files from `skills/` as Project Knowledge, or add them as Project Skills if your workspace supports that directly.
3. Start a conversation in the project. The orchestrator skill fires on every new request and decides which of the other seven apply.

## Claude Code

1. Copy the `skills/` folder into your project, or into your global skills directory.
2. Each `SKILL.md` needs to sit in its own folder, named after the skill (e.g. `orchestrator/SKILL.md`), matching the structure already used in this repo.
3. Claude Code picks these up automatically, the same way it does with any other skill.

## Adjusting for your setup

Two things are worth reviewing before relying on this daily:

- `state-sync` assumes a personal note system for the narrative journal (Obsidian, Notion, or similar). Without one, it falls back to a local `journal.md`. If your repo is public, decide upfront whether `STATE.md` and `journal.md` should be tracked or excluded via `.gitignore`.
- `orchestrator`'s trivial/non-trivial definition is a starting point, not a universal rule. Adjust it if your own sense of "worth pausing for" differs.

## A note on reliability

This stack runs on the assistant actually following its own instructions, session after session. There's no hook or CI gate that enforces it from outside. See the article series linked in the README for where and why that can fail, and what the visibility line in `orchestrator` does (and doesn't) do about it.
