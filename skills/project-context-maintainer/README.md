# Project Context Maintainer

A portable skill for coding agents that keeps project knowledge durable across chats and sessions.

## Files included

- `SKILL.md` — agent instructions and lifecycle workflow.
- `templates/handover.md`
- `templates/decisions.md`
- `templates/flow.md`
- `templates/architecture.md`
- `templates/bugs.md`
- `templates/features.md`
- `templates/constraints.md`

## Use in a coding agent

1. Add the `project-context-maintainer` folder to the agent's skills directory, or copy `SKILL.md` into the skill format your agent supports.
2. Ensure the agent is instructed to load/use this skill for repository work.
3. At the start of a project, ask the agent to initialize the seven project context files from the templates. For an existing project, it should inspect and reuse equivalent documentation rather than creating duplicates.
4. Keep the skill available for subsequent sessions so the agent reads `handover.md` before continuing.

The skill is tool-agnostic. It does not depend on a specific model, IDE, terminal, or coding agent. The agent still needs repository read/write access to create and update project files.
