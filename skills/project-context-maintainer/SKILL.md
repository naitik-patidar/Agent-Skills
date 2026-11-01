---
name: project-context-maintainer
description: Maintain durable, accurate project context for coding agents across sessions. Use when exploring, modifying, debugging, reviewing, or handing off a software project so future agents can understand the current state, decisions, execution flow, architecture, bugs, features, and constraints without reconstructing everything from scratch.
---

# Project Context Maintainer

## Purpose

Keep the project's operational knowledge outside the chat so that a new coding agent, a new chat, or a human collaborator can continue the work without starting from zero.

Treat project documentation as part of the implementation, not as optional end-of-task paperwork. Write it incrementally as facts are discovered and decisions are made. Keep it concise, current, linked to source files, and honest about what has and has not been verified.

## Canonical project files

Unless the repository already has an established equivalent structure, maintain these seven Markdown files at the repository root:

1. `handover.md` — current state and cold-start instructions for the next session.
2. `decisions.md` — important decisions and, especially, why they were made.
3. `flow.md` — concrete execution paths across entry points, files, functions, services, and data stores.
4. `architecture.md` — the system map, boundaries, components, integrations, and dependencies.
5. `bugs.md` — bug reports, investigation notes, root causes, fixes, and verification.
6. `features.md` — feature requests, acceptance criteria, implementation status, and verification.
7. `constraints.md` — hard boundaries, invariants, compatibility requirements, and things agents must not change.

The user once called the final file `contrast.md`, but their detailed description defines `constraints.md`. Use `constraints.md` as the canonical name. Do not create a second `contrast.md` unless the user explicitly explains a separate purpose for it.

Use the exact names already established by a repository if it has an equivalent documentation convention. Do not create duplicate files just because capitalization, singular/plural, or folder placement differs. For example, an existing `DECISIONS.md` may serve the same purpose as `decisions.md`.

If a repository intentionally stores project documentation in a dedicated folder (for example, `docs/` or `.project/`), follow that convention and record the location in `handover.md`. Otherwise, use the repository root so any coding agent can discover the files easily.

## Operating rules

### 1. Discover before changing

At the beginning of a project or a new task:

- Inspect the repository structure, README, agent instructions, package/build files, tests, and relevant source files.
- Check for existing project-context documents and read them before making changes.
- Respect `AGENTS.md`, `CLAUDE.md`, `CONTRIBUTING.md`, local instructions, and user-provided constraints. These instructions take precedence over this skill.
- Determine the current branch and working-tree state when the environment allows it. Never overwrite or discard pre-existing user changes.
- Identify what is known, what is inferred, and what remains unknown. Do not present guesses as facts.

If context files do not exist, create all seven using the templates in this skill. If some are not relevant yet, keep a short status such as “No known entries yet; update when applicable” rather than inventing content.

### 2. Update incrementally

Do not wait until the end of the session.

- Add a decision to `decisions.md` when a meaningful architectural, design, dependency, data, API, security, or implementation choice is made.
- Update `architecture.md` when a component, boundary, dependency, data store, deployment path, or integration is discovered or changed.
- Update `flow.md` when the execution path is discovered or changed. Trace the actual path, not an imagined ideal path.
- Add or update a bug entry as soon as a defect is identified; record investigation progress and later the verified root cause and fix.
- Add or update a feature entry when scope or acceptance criteria are agreed, then record implementation and verification.
- Update `constraints.md` as soon as a hard boundary or invariant is discovered.
- Refresh `handover.md` throughout longer sessions and before ending any meaningful session.

### 3. Keep facts traceable

- Reference concrete repository paths, symbols, commands, endpoints, configuration keys, and test names wherever possible.
- Include line numbers only when they have been checked and are useful; line numbers can become stale.
- Distinguish `Verified`, `Inferred`, `Unknown`, `Blocked`, and `Not tested` where the distinction matters.
- Never claim a test passed unless it was actually run and its result observed.
- Never claim a bug is fixed unless the relevant behavior was verified. If only a code change was made, say “change made; verification pending.”
- Do not store secrets, access tokens, private keys, passwords, or sensitive personal data in these files. Refer to environment-variable names or secret-manager locations instead.
- Do not copy large source files into documentation. Explain the relevant behavior and link to the source.

### 4. Avoid documentation drift and duplication

- Keep each fact in its natural home and link to it from other files when needed.
- `handover.md` is the current snapshot, not a second full architecture document.
- `decisions.md` records rationale; `architecture.md` records the resulting system shape.
- `flow.md` explains runtime behavior; `architecture.md` explains the structural map.
- `bugs.md` tracks defects; `features.md` tracks desired capabilities and delivery.
- `constraints.md` records boundaries that future changes must preserve.
- When information changes, update or mark the old information as superseded. Do not silently leave contradictory statements in active sections.
- Prefer dated, append-only records for decisions and audit history. Edit current-state summaries when the state changes.
- Keep docs useful to a cold-start reader. Avoid chat transcripts, vague claims, and unexplained abbreviations.

### 5. Protect the repository

- Documentation does not authorize code changes. Follow the user's task and repository instructions.
- Never modify files listed as protected in `constraints.md` without explicit authorization.
- Do not run destructive commands, rewrite history, delete data, rotate credentials, change production infrastructure, or perform irreversible migrations unless explicitly authorized.
- Do not weaken tests, validation, security checks, or access controls merely to make a task pass.
- Preserve public APIs, data formats, migrations, and compatibility guarantees unless the task explicitly requires changing them.
- If a task conflicts with a recorded constraint, stop that portion, explain the conflict, and ask for direction where needed.

## Session workflow

### Phase A — Start / recover context

1. Read the canonical context files and repository instructions.
2. Read the latest handover first, then validate its claims against the actual working tree and code.
3. Check whether the stated branch, changed files, tests, and outstanding tasks are still accurate.
4. Identify the current task, its scope, and applicable constraints.
5. If the handover is missing or stale, repair it from verifiable repository evidence before proceeding.

### Phase B — Explore and plan

1. Locate the true entry point(s) and relevant execution path.
2. Map affected components and their dependencies before editing.
3. Record significant decisions and their rationale, including alternatives considered and trade-offs.
4. Define acceptance criteria for feature work or reproduction/expected behavior for bug work.
5. Identify risks, protected areas, and verification steps.

### Phase C — Implement and document as you go

1. Make the smallest change that satisfies the task and respects constraints.
2. Update `flow.md` and `architecture.md` when the actual implementation changes the execution path or system structure.
3. Update `decisions.md` when a non-obvious choice is made. Record rejected alternatives when they would otherwise be reconsidered later.
4. Keep bug/feature status current, including blockers and partial completion.
5. Add or refine tests where appropriate. Record commands and actual outcomes.
6. Keep `handover.md` current during long tasks, especially before context switches.

### Phase D — Close the session

Before ending a meaningful coding session:

1. Reconcile all seven documents with the actual code and working-tree state.
2. Update `handover.md` last so it reflects the final state of the session.
3. List files changed, work completed, work not completed, open questions, blockers, risks, and exact next steps.
4. Record verification commands and results. Separate tests run from tests not run.
5. Confirm that no secrets or sensitive values were written into documentation.
6. Do not claim the repository is clean unless you checked it.

A session is not complete until the handover is useful to a fresh agent who has not seen the conversation.

## Required content by file

### `handover.md`

Maintain a concise, current snapshot with:

- Last updated date/time and timezone, if known.
- Project purpose and current task/objective.
- Current branch and working-tree state, if known.
- Current implementation state and important recent changes.
- Files/modules touched and why.
- Work completed and work remaining.
- Current blockers, risks, and unresolved questions.
- Tests/checks run, exact commands, and observed results.
- Important constraints to read before editing.
- Ordered next steps that a fresh agent can execute.
- Links to relevant decisions, flow sections, bugs, and features.

Make the next action obvious. Do not force a new agent to infer where to begin.

### `decisions.md`

For every meaningful decision, record:

- ID and date.
- Status: Proposed, Accepted, Superseded, or Rejected.
- Context/problem.
- Decision made.
- Why it was chosen.
- Alternatives considered and why they were not chosen.
- Consequences, trade-offs, and risks.
- Affected paths/components and links to related decisions.

Record the reasoning, not merely the final technology or pattern. Do not log trivial syntax choices.

### `flow.md`

Document real execution flows in ordered steps. For each important flow, include:

- Trigger or entry point (route, CLI command, event, scheduled job, UI action, webhook, etc.).
- File and symbol at each step.
- Calls between functions, modules, services, and external systems.
- Data passed, transformed, validated, persisted, or returned.
- Branches, error handling, retries, and important side effects.
- Response/output and relevant tests.

Use Mermaid only when it materially clarifies the flow, and provide a short text explanation too. Mark unverified parts as inferred or unknown.

### `architecture.md`

Maintain a navigable system map containing:

- What the system does and its major use cases.
- High-level component map and responsibilities.
- Important directories and entry points.
- Runtime, frameworks, languages, build/test tooling, and deployment shape when known.
- Data stores, schemas, queues, caches, and ownership of data.
- Internal and external integrations, APIs, and trust boundaries.
- Authentication, authorization, secrets handling, and security-sensitive components at a high level.
- Important dependencies and coupling points.
- Links to detailed execution flows and decisions.

Do not invent architecture from framework conventions; inspect the actual code and configuration.

### `bugs.md`

For each known defect, track:

- Bug ID, title, status, priority/severity, and date discovered.
- Affected versions, modules, paths, or environments when known.
- Reproduction steps and frequency.
- Expected behavior versus actual behavior.
- Evidence: logs, error messages, screenshots, test names, or observed output (without secrets).
- Investigation notes and hypotheses, clearly labeled.
- Verified root cause, or state that it is still unknown.
- Fix and affected files/commit reference when available.
- Regression coverage and verification result.
- Remaining risk or follow-up.

Suggested statuses: Open, Investigating, Blocked, Fixed-Unverified, Verified-Fixed, Won't-Fix, or Duplicate.

### `features.md`

For each meaningful feature or enhancement, track:

- Feature ID, title, status, and date added.
- User/problem statement and desired outcome.
- Scope and explicit non-goals.
- Acceptance criteria that can be checked.
- Dependencies and constraints.
- Implementation plan or affected components.
- Actual implementation and paths changed.
- Tests/verification and result.
- Follow-ups, known limitations, and release notes if relevant.

Suggested statuses: Proposed, Planned, In Progress, Blocked, Implemented-Unverified, Verified, Deferred, or Rejected.

### `constraints.md`

Make hard boundaries explicit and actionable. Include:

- User- or project-imposed non-negotiable requirements.
- Protected files, directories, services, and ownership boundaries.
- Public API, schema, protocol, and backward-compatibility invariants.
- Security/privacy rules and secret-handling requirements.
- Database migration, data-retention, and production-operation restrictions.
- Performance, platform, dependency, licensing, or deployment limits.
- Required approvals before a risky or irreversible action.
- Known forbidden approaches and the reason they are forbidden.

For each constraint, state its source (user instruction, repository policy, technical invariant, compliance requirement, or observed dependency), scope, and what explicit authorization would be needed to change it. Do not invent restrictions; mark assumptions as assumptions until confirmed.

## Interaction with the user

- Do not ask the user to repeat facts already present in the repository or handover.
- Ask a question only when a missing decision materially blocks safe progress. Otherwise make a conservative, reversible assumption and record it as an assumption.
- Surface conflicts between user instructions, repository instructions, and recorded constraints clearly.
- At completion, provide a short human-readable summary and point to the context files updated. Mention any sections that remain unknown or unverified.
- Never imply that the documentation files were updated if they were not.

## Definition of done

For a meaningful coding task, all of the following should be true:

- [ ] Existing context and repository instructions were read.
- [ ] Code changes satisfy the requested scope and recorded constraints.
- [ ] `architecture.md` and `flow.md` reflect any affected structural/runtime changes.
- [ ] `decisions.md` captures meaningful decisions and their rationale.
- [ ] Relevant bug/feature records are current.
- [ ] `constraints.md` reflects discovered or changed hard boundaries.
- [ ] `handover.md` accurately describes the final state and next steps.
- [ ] Tests and checks are reported truthfully, including anything not run.
- [ ] No secrets or sensitive values were added to documentation.

For a tiny change with no impact on architecture, flow, decisions, bugs, or features, do not fabricate updates. Still check whether the handover needs a brief refresh, and say why the other files were unchanged.

## Templates

Use the templates in the `templates/` directory of this skill as starting points. Adapt them to the repository instead of overwriting useful project-specific structure.
