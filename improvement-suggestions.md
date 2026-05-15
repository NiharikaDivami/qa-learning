# Improvement Suggestions

Recommendations to harden the platform, grouped by priority. Each suggestion notes the rationale (linked defect or risk where applicable).

## High priority

- **Server-side duplicate detection on (vendor, invoice_number)**
  Prevents double-payment seen in [DEF_001](defect-reports.csv) and addresses [R_01](risk-register.csv).

- **Immutable audit log for approvals, rejections, and resubmissions**
  Required for financial compliance and root-cause analysis. Today the audit trail is incomplete (see [R_13 in earlier draft]; now covered by REQ_19 in [rtm.csv](rtm.csv)).

- **Retry-with-backoff and dead-letter queue for failed notifications**
  Notification failures are silent today ([DEF_004](defect-reports.csv)). Vendors lose visibility into status changes.

- **Strengthen file-upload validation (mime sniffing + content scan)**
  Extension-based check is bypassable ([DEF_009](defect-reports.csv)). Allowlist mime types and scan content.

- **Row-level security at the DB layer in addition to application checks**
  Defense in depth against IDOR / cross-tenant bugs ([DEF_003](defect-reports.csv), [R_04](risk-register.csv)).

- **Rotate session id on login and enforce idle timeout**
  Addresses session-reuse defect ([DEF_006](defect-reports.csv)) and [R_07](risk-register.csv).

- **E2E smoke test running against staging on every deploy**
  Catches integration regressions before prod — the bulk of the defects above would have been caught by a single happy-path E2E run.

## Medium priority

- **Improve error messages to specify which field failed and how to fix it**
  Reduces vendor support tickets and resubmission churn.

- **Support idempotency-keys on invoice creation**
  Protects against duplicate submissions caused by client retries (see also [GAP_10](requirement-gaps.md)).

- **Configurable amount threshold for two-person approval**
  Reduces blast radius of accidental or malicious approvals.

- **Async report generation with email-when-ready for large reports**
  Avoids timeouts on full-year reports.

- **Emit metrics for invoice lifecycle and notification success rate**
  Enables proactive detection of regressions before users notice.
