# Vendor Invoice Processing Platform — QA Deliverables

QA artifacts for the Vendor Invoice Processing Platform evaluation. The reference brief (system overview, assumptions, risk areas, and approach) is in [vendor-portal-assignment.md](vendor-portal-assignment.md).

Format choice:
- **CSV** for matrix-shaped artifacts that benefit from sort, filter, and import into test-management tools (test cases, scenarios, RTM, risks, defects).
- **Markdown** for narrative artifacts that are read top-to-bottom rather than filtered (open questions, recommendations).

## Index

| Artifact | File | Purpose |
| --- | --- | --- |
| Brief / QA approach | [vendor-portal-assignment.md](vendor-portal-assignment.md) | Scope, assumptions, risks, approach |
| Test scenarios (high level) | [test-scenarios.csv](test-scenarios.csv) | One-line scenarios mapped to modules |
| Test cases | [test-cases.csv](test-cases.csv) | All detailed test cases — filter by `Module` |
| Defect reports | [defect-reports.csv](defect-reports.csv) | Sample bugs with steps, severity, environment |
| Requirements Traceability Matrix (RTM) | [rtm.csv](rtm.csv) | Requirements → scenarios → cases → defects |
| Risk register | [risk-register.csv](risk-register.csv) | Risks with likelihood, impact, mitigation, linked tests |
| Requirement gaps | [requirement-gaps.md](requirement-gaps.md) | Open questions to clarify with product |
| Improvement suggestions | [improvement-suggestions.md](improvement-suggestions.md) | Recommendations to harden the platform |

## Test coverage at a glance

Test cases in [test-cases.csv](test-cases.csv) are grouped by `Module`:

| Module | Count | Focus |
| --- | --- | --- |
| Authentication | 7 | Login, lockout, session, password reset |
| Invoice Upload | 9 | PO linkage, validation, duplicates, resubmission |
| Invoice Processing | 8 | Approval, rejection, concurrency, payment routing, audit |
| Notifications | 5 | Status emails, retry, content correctness |
| Reporting | 4 | Monthly report, accuracy, filtering, role scope |
| Edge Case | 4 | Duplicates, interruption, session expiry, notification failure |
| API | 10 | Status codes, required fields, authorization, expired tokens |
| Database | 8 | Persistence, mapping, vendor isolation, constraints, audit log |
| Security | 7 | RBAC, cross-tenant, IDOR, brute-force, file upload |

## ID conventions

- `TS_*` — test scenario (high-level, in `test-scenarios.csv`)
- `TC_AUTH_*`, `TC_UPL_*`, `TC_PROC_*`, `TC_NOTIF_*`, `TC_RPT_*`, `TC_EDGE_*`, `TC_API_*`, `TC_SEC_*` — detailed test cases by module
- `DB_*` — database-layer validation checks
- `DEF_*` — defect reports
- `REQ_*` — requirements (in RTM)
- `R_*` — risk register entries
- `GAP_*` — open requirement clarifications

## How to use

1. Start with [vendor-portal-assignment.md](vendor-portal-assignment.md) for context and the QA approach.
2. Use [test-scenarios.csv](test-scenarios.csv) for a single-page view of what's covered.
3. Drill into [test-cases.csv](test-cases.csv) (filter by `Module`) for executable steps and expected results.
4. Use [rtm.csv](rtm.csv) to confirm every requirement is covered — or flagged as a gap.
5. Use [requirement-gaps.md](requirement-gaps.md) as the agenda for the next product clarification meeting.
6. Use [risk-register.csv](risk-register.csv) and [improvement-suggestions.md](improvement-suggestions.md) when prioritizing hardening work alongside feature development.
