---
name: Return carrier EOI decisions to PlanSource
description: As a carrier or underwriting partner, pull employees with pending Evidence of Insurability
  and post approve/deny decisions and form completions back.
api: openapi/plansource-admin-api-openapi-original.json
base_url: https://api.plansource.com/admin/v2
operations:
- GET /eoi/subscribers
- GET /eoi/subscriber/{subscriber_id}
- PUT /eoi/decisions
- PUT /eoi/decision/{subscriber_id}
- PUT /eoi/form_completions
- PUT /eoi/form_completion/{subscriber_id}
- GET /coverage/subscriber/{subscriber_id}
---

# Return carrier EOI decisions to PlanSource

## When to use this
You are the carrier (or the underwriting platform) on a life/disability product where elected volume exceeds the guaranteed-issue amount. PlanSource holds the pending EOI; you hold the decision.

## The flow
1. **Pull the queue** — `GET /eoi/subscribers` for everyone pending, `GET /eoi/subscriber/{subscriber_id}` for one. Filter with `plan_year` and `changes_since`.
2. **Record form receipt** — `PUT /eoi/form_completions` (batch) or `PUT /eoi/form_completion/{subscriber_id}` (single) once the employee's health questionnaire is in. This is a separate step from the decision; skipping it leaves the employee's portal showing an outstanding form.
3. **Post the decision** — `PUT /eoi/decisions` (batch) or `PUT /eoi/decision/{subscriber_id}` (single). The batch body is keyed on `ssn` + `benefit_lookup_code` with an `action` (e.g. `approve_all`), `approved_volume`, `effective_date` and `original_effective_date`.
4. **Verify** — `GET /coverage/subscriber/{subscriber_id}` and confirm the approved volume landed on the coverage.

## Rules that will bite you
- **Read the batch response row by row.** A 200 carries `data.valid_count`, `data.failed_count` and `data.failed_rows` — a row can fail with `"errors": "Employee not found"` while the call itself succeeded. Treat `failed_count > 0` as a partial failure, not a success.
- **Match on `ssn` + `benefit_lookup_code`, not on a name.** Those two fields are the documented natural key for the batch payload.
- **`approved_volume` is a decimal string** (`"125000.00"`), and **an approval for less than the elected amount is a partial approval** — send the amount you actually approved, not the amount requested.
- **There is no idempotency key and this operation is irreversible.** Posting the same approval twice is a real risk on retry. Re-read with `GET /eoi/subscribers` before resending; a subscriber that has left the pending queue has already been decided.
- `effective_date` vs `original_effective_date` are different fields with different meanings — `set_original_effective_date` on the coverage endpoints controls which one a downstream recalculation uses.
- This carries PHI and underwriting outcomes. Never log the body.
