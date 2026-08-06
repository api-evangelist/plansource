---
name: Create, stack, and terminate benefit coverages
description: Work with coverages, stacked coverage lines, dependent coverages and beneficiary allocations
  for an employee.
api: openapi/plansource-admin-api-openapi-original.json
base_url: https://api.plansource.com/admin/v2
operations:
- GET /coverage/meta
- POST /coverage
- GET /coverage/{coverage_id}
- PUT /coverage/{coverage_id}
- PUT /coverage/{coverage_id}/terminate
- POST /coverage/{coverage_id}/line
- GET /coverage/{coverage_id}/lines
- PUT /coverage/line/{coverage_line_id}/terminate
- POST /coverage/{coverage_id}/dependent
- GET /coverage/{coverage_id}/dependents
- PUT /coverage/dependent/{dependent_coverage_id}/terminate
- GET /coverage/{coverage_id}/beneficiaries
- PUT /coverage/{coverage_id}/beneficiaries
- POST /coverage/{coverage_id}/beneficiaries
- DELETE /coverage/{coverage_id}/beneficiaries
- GET /coverage/subscriber/{subscriber_id}
- GET /coverage/subscriber/{subscriber_id}/composite
- PUT /coverage/subscriber/{subscriber_id}/terminate
- GET /coverage/composites
---

# Create, stack, and terminate benefit coverages

## When to use this
You need to read or write what an employee is actually enrolled in — the coverage itself, the stacked lines inside it, who is covered under it, and who inherits it.

## The shape of the model
`Subscriber` → many `Coverage` → many `CoverageLine` (stacked volumes) and many `DependentCoverage` (who is covered) and many `Beneficiary` (who inherits). See `data-model/plansource-data-model.yml`.

## The flow
1. `GET /coverage/meta` — the valid enumerations. Read it first, same discipline as the demographic meta.
2. **Read what exists** — `GET /coverage/subscriber/{subscriber_id}`. For anything non-trivial prefer **`GET /coverage/subscriber/{subscriber_id}/composite`**: one call returns the coverage plus its supporting objects, instead of a fan-out of six. `GET /coverage/composites` is the population-wide version.
3. **Create** — `POST /coverage`, or `POST /coverage/{coverage_id}/line` to stack a line onto an existing coverage.
4. **Cover dependents** — `POST /coverage/{coverage_id}/dependent`; list with `GET /coverage/{coverage_id}/dependents`.
5. **Beneficiaries** — `GET|POST|PUT|DELETE /coverage/{coverage_id}/beneficiaries`. Allocations are percentages and **must total 100 across the primary beneficiaries**; `primary_beneficiary` distinguishes primary from contingent.
6. **Terminate** — narrowest scope that does the job: a line (`PUT /coverage/line/{coverage_line_id}/terminate`), a dependent's coverage (`PUT /coverage/dependent/{dependent_coverage_id}/terminate`), one coverage (`PUT /coverage/{coverage_id}/terminate`), or everything for the employee (`PUT /coverage/subscriber/{subscriber_id}/terminate`).

## Rules that will bite you
- **`PUT /coverage/subscriber/{subscriber_id}/terminate` and `DELETE /coverage/{coverage_id}/beneficiaries` are the destructive pair in this API.** They are wide, they are not idempotent, and there is no undo endpoint. Confirm scope against a fresh composite read before sending, and treat both as human-approval operations in an agent context (see `agentic-access/plansource-agentic-access.yml`).
- `recalculate`, `recalculate_volume` and `validate_volume` change what the call *does*, not just what it returns. `validate_volume` checks an elected volume against plan maximums — use it before creating a coverage you expect to trip guaranteed-issue, which is what routes the employee into EOI.
- `set_change_effective_date` and `set_original_effective_date` control which effective date the change is anchored to. Getting these wrong retroactively re-rates premiums.
- Always pass `plan_year`.
