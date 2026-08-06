---
name: Sync employee demographics from an HCM into PlanSource
description: Create, update, terminate and rehire employees (subscribers) and their dependents so an HCM/payroll
  system of record stays in sync with PlanSource benefits.
api: openapi/plansource-admin-api-openapi-original.json
base_url: https://api.plansource.com/admin/v2
operations:
- GET /organizations
- GET /subscriber/meta
- POST /subscribers
- GET /subscribers
- PUT /subscribers
- GET /subscriber/{id}
- PUT /subscriber/{id}
- PUT /subscriber/{id}/terminate
- PUT /subscriber/{id}/rehire
- POST /subscriber/{subscriber_id}/dependent
- PUT /subscriber/{subscriber_id}/dependent/{id}
- PUT /subscriber/{subscriber_id}/dependent/{id}/deactivate
- GET /dependent/meta
---

# Sync employee demographics from an HCM into PlanSource

## When to use this
Your HCM or payroll platform is the system of record for employee data and PlanSource administers the benefits. Use this skill to push new hires, demographic changes, terminations and rehires into PlanSource, plus the dependents that drive eligibility.

## Before you call anything
1. Get a token: `POST https://api.plansource.com/oauth/v2/token`, OAuth 2.0 **client credentials**, scope `admin_api_v2`. (The legacy alternative is the `AuthenticationString` + `Signature` header pair — both headers together, never one alone.)
2. Point at the right host. Build against **`https://partner-dev-api.plansource.com/admin/v2`**; only move to `https://api.plansource.com/admin/v2` once the client is configured and implemented.
3. `GET /organizations` first. It returns exactly the organizations this API user may act on. Every other call is scoped to one of them — a 403 later almost always means you addressed a record outside this list.
4. `GET /subscriber/meta` and `GET /dependent/meta` return the valid enumerations (division, org_class, location, employment_level, union_code, state, country, gender, marital_status, termination reasons). **Read these before writing.** Sending a value outside the meta set is the most common 400.

## The flow
- **New hire** — `POST /subscribers` for a batch, `POST /subscriber` for one. Batch is strongly preferred for a nightly sync.
- **Change** — `PUT /subscribers` for a batch, `PUT /subscriber/{id}` for one. Add `is_custom_id=true` when `{id}` is your own employee id rather than a PlanSource id; that flag is what lets you avoid storing PlanSource ids at all.
- **Termination** — `PUT /subscriber/{id}/terminate` (or `PUT /subscribers/terminate`). Supply a valid termination reason from `GET /subscriber/meta`. Termination is the trigger for downstream coverage termination — do not separately terminate coverages unless you intend to.
- **Rehire** — `PUT /subscriber/{id}/rehire` (or `PUT /subscribers/rehire`). Rehire, not create: creating a second subscriber for a returning employee splits their history.
- **Dependents** — `POST /subscriber/{subscriber_id}/dependent`, then `PUT .../dependent/{id}` for changes. Removing a dependent is `PUT .../dependent/{id}/deactivate`, never a delete; `.../reactivate` undoes it.
- **Incremental reads** — `GET /subscribers?changes_since=<timestamp>` to pull only what moved. Add `plan_year` to scope, and `include_test=true` only when you deliberately want test employees.

## Rules that will bite you
- **There is no idempotency key.** PlanSource publishes no `Idempotency-Key` header. A bulk `PUT /subscribers` that times out mid-flight may be *partially* applied. Do not blind-retry: re-read with `GET /subscribers?changes_since=` and reconcile before resending.
- **Paging returns no metadata.** `page` (default 1) and `per_page` (default and max-ish 500) are all you get — no total, no next link. Page until a short page comes back.
- **Bulk responses are per-row.** A 200 on a collection write does not mean everything succeeded. Read `data.valid_count`, `data.failed_count` and `data.failed_rows` in the body.
- **Errors are not RFC 9457.** The envelope is `{status, http_status, message, details, error_code, errors, data}` as `application/json`. Branch on `error_code` (e.g. `missing.required.attribute`, `date.not.valid`), not on prose in `message`.
- Dates are `YYYY-MM-DD`; a bad format returns 400 `date.not.valid`.
- **This is HIPAA-regulated PHI.** Log `error_code` and record ids, never payload bodies.
