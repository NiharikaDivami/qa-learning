# Requirement Gaps & Open Clarifications

Open questions that need a product/finance/engineering decision before tests can be finalized. Each gap notes why it matters and which test cases are blocked by it.

## Invoice Upload

- **GAP_01 — Can multiple invoices be submitted against a single PO?**
  Affects partial-billing flow. Without a rule, vendors could over-bill or be blocked unnecessarily.
  _Blocks: TC_UPL_006_ · Owner: Product

- **GAP_02 — Is there an upper limit on invoice amount relative to the PO balance?**
  Determines whether the system blocks over-PO invoices or routes them to AP for tolerance review.
  _Blocks: TC_UPL_006_ · Owner: Product / Finance

- **GAP_04 — Which file types are supported (PDF, Excel, images)?**
  Drives validation rules and the file-upload allowlist.
  _Blocks: TC_UPL_004_ · Owner: Product

- **GAP_05 — Maximum file upload size?**
  Drives boundary test and storage planning.
  _Blocks: TC_UPL_005_ · Owner: Product

- **GAP_11 — Are draft invoices supported (save and resume)?**
  Defines behavior when session expires mid-form.
  _Blocks: TC_EDGE_003_ · Owner: Product

## Invoice Processing

- **GAP_03 — Can rejected invoices be modified and resubmitted?**
  Changes the lifecycle state machine and notification rules.
  _Blocks: TC_UPL_009_ · Owner: Product

- **GAP_07 — Can multiple AP users act on the same invoice simultaneously?**
  Defines the concurrency model — first-write-wins vs lock vs queue.
  _Blocks: TC_PROC_005_ · Owner: Product

- **GAP_12 — Does an invoice expire after N days in SUBMITTED state?**
  Stale invoices may need auto-cancellation; impacts SLA reporting.
  _No test yet_ · Owner: Product

## Notifications

- **GAP_06 — How should the system handle email delivery failures?**
  Defines retry policy, SLA, and admin visibility for failed sends.
  _Blocks: TC_NOTIF_004_ · Owner: Product / DevOps

## Authorization

- **GAP_09 — Can AP role submit invoices on behalf of a vendor?**
  Determines API authorization rules for invoice creation.
  _Affects API test scope_ · Owner: Product

- **GAP_13 — Can a vendor download files attached to their approved invoices indefinitely?**
  Retention and access window must be defined.
  _No test yet_ · Owner: Product / Compliance

- **GAP_15 — Is the audit log accessible to vendors, AP users, or both?**
  Drives UI and authorization on audit endpoints.
  _Affects TC_PROC_008_ · Owner: Product

## Reporting & Data

- **GAP_08 — What time zone is the monthly cut-off based on?**
  Invoices created around midnight could land in the wrong month.
  _No test yet_ · Owner: Product

- **GAP_14 — Is multi-currency supported for invoices?**
  Determines validation, FX handling, and reporting.
  _No test yet_ · Owner: Product / Finance

## API

- **GAP_10 — Is an idempotency-key supported on invoice creation?**
  Protects against duplicate submissions when clients retry on network errors.
  _No test yet_ · Owner: Backend
