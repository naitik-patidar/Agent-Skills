# Execution Flows

> Document how the application actually executes across files, symbols, services, and data stores.

## Flow index
| Flow | Trigger | Entry point | Status |
|---|---|---|---|
| [Flow name] | [UI action / API / CLI / event] | `path:Symbol` | Verified / Partial / Inferred |

## FLOW-001 — [Flow name]
- **Status:** Verified / Partial / Inferred
- **Trigger:** [What starts this flow]
- **Entry point:** `path/to/file:Symbol`

### Steps
1. `path/to/file:Function` — [what happens; input/output]
2. `path/to/other_file:Function` — [call and transformation]
3. [Service/API/database] — [request, persistence, side effect, or response]

### Branches and failures
- [Validation, authorization, retries, exceptions, fallback paths]

### Data and side effects
- [Important data shape, state changes, persistence, emitted events]

### Output
- [Response, UI update, job result, or observable behavior]

### Verification
- **Tests/checks:** [names or commands]
- **Evidence:** [observed result]

### Related
- Architecture: [section/link]
- Decisions: [IDs]
- Bugs/features: [IDs]

---

_No execution flows documented yet._
