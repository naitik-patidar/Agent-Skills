# Agent Skills

A collection of reusable skills for AI coding agents and other agentic workflows.

## Available skills

| Skill | Description | Location |
|---|---|---|
| [Project Context Maintainer](skills/project-context-maintainer/) | Keeps project handovers, decisions, execution flows, architecture, bugs, features, and constraints documented across coding sessions. | `skills/project-context-maintainer/` |

## Adding another skill

1. Create a new folder under `skills/` using a lowercase, kebab-case name.
2. Add a `SKILL.md` with the skill's instructions and metadata/frontmatter required by the target agent ecosystem.
3. Add a `README.md` explaining the skill's purpose, contents, and usage.
4. Put reusable templates, examples, scripts, or references in subfolders inside that skill's folder.
5. Add the new skill to the table above.

Keep each skill self-contained so it can be copied into a coding agent's supported skills directory independently.
