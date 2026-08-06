---
name: Pull payroll deductions back into the payroll system
description: Retrieve per-employee benefit deductions, their lookup codes, and the pre-tax, post-tax,
  employer and imputed-income amounts, so payroll can apply them.
api: openapi/plansource-admin-api-openapi-original.json
base_url: https://api.plansource.com/admin/v2
operations:
- GET /organizations
- GET /payroll_coverages_subscribers
- GET /payroll_coverages_subscriber/{id}
- GET /subscribers
---

# Pull payroll deductions back into the payroll system

## When to use this
PlanSource is the system of record for benefit elections; your payroll engine needs the resulting deductions each pay cycle. This is the read half of the round trip whose write half is the demographics sync.

## The flow
1. `GET /organizations` — confirm scope.
2. `GET /payroll_coverages_subscribers` — the whole population for a `plan_year`. Page with `page` / `per_page` (default 500).
3. `GET /payroll_coverages_subscriber/{id}` — one employee, for reconciliation or an off-cycle correction. `is_custom_id=true` if `{id}` is your payroll id.

## Reading the payload
Each deduction carries a **deduction lookup code** plus separate pre-tax, post-tax, employer and imputed-income amounts. Map on the lookup code — it is the stable cross-system join key. Do **not** map on the plan display name; names get re-labelled at renewal, codes do not.

## Rules that will bite you
- **Always send `plan_year`.** It appears on 31 of the 80 operations and is the single most important filter. During open enrollment two plan years are live at once; omitting it is how you deduct the wrong year's premium.
- Use `changes_since` for incremental pulls, but run a **full** reconciliation pull each cycle before you commit a payroll file. There is no webhook and no event stream — polling is the only change signal PlanSource offers, and a missed poll is a silently missed deduction.
- `start_date` / `end_date` bound the effective window; `recalculate` re-derives amounts rather than returning the stored ones — know which you want before you send it.
- Imputed income is a taxable amount, not a deduction. Do not sum it into the employee's withholding.
