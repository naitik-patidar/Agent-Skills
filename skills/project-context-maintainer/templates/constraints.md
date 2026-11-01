# Constraints

> Hard boundaries and invariants that every agent must preserve unless the authorized person explicitly changes them.

## Constraint index
| ID | Constraint | Source | Scope | Change approval |
|---|---|---|---|---|
| CON-001 | [Short statement] | User / Repository policy / Technical invariant / Compliance / Assumption | [Scope] | [Who or what approval is required] |

## CON-001 — [Title]
- **Status:** Active / Superseded / Needs confirmation
- **Source:** User instruction / Repository policy / Technical invariant / Compliance requirement / Assumption
- **Rule:** [Specific actionable boundary]
- **Reason:** [Why it exists]
- **Scope:** [Files, components, data, environments, or operations covered]
- **Forbidden actions:** [What the agent must not do]
- **Allowed actions:** [What remains safe/allowed]
- **Approval to change:** [Explicit authorization required]
- **Related:** [Paths, decisions, architecture sections]

## Protected files and areas
| Path / area | Protection | Required authorization |
|---|---|---|
| [Path] | [Do not edit / generated / owned by another system / sensitive] | [Approval] |

## Compatibility and data invariants
- [Public API, schema, protocol, migration, backward-compatibility requirements]

## Security and privacy boundaries
- [No secrets in docs/logs; auth requirements; sensitive-data handling]

## Operational restrictions
- [Production, destructive commands, migrations, deployment, resource limits]

## Assumptions requiring confirmation
- [Clearly label anything not yet confirmed]

---

_No confirmed constraints recorded yet. Do not treat absence of entries as permission for destructive or irreversible actions._
