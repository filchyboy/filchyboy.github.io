---
layout: post
title: "Daily Dev Log - 2026-07-01"
date: 2026-07-01
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-07-01T12:15:47.628166+00:00 -->

## Today's Plan

Wednesday. The operational-intelligence-workspace plan landed its scaffold yesterday and is sitting at 0/47 tracker items — it's time to actually start executing on it. The react-doctor sprint and PHPStan remediation are both in motion and need forward progress too.

### Main Focus

**Begin execution on `oiw-confirm-boundaries-and-source-contracts`** — The OIW plan was scaffolded yesterday (status: in-progress, started 1 day ago, 0% complete), so the planning infrastructure is solid but no implementation has happened yet. This first item is the right starting point for a concrete reason: the schema work downstream (`oiw-design-projection-schema`, `oiw-create-observation-projection-migration`, `oiw-create-evidence-reference-migration`) can't land in the right container without a confirmed boundary. Getting the container boundary wrong at migration time is a schema cleanup problem that compounds — I've seen this play out in regime-compliance-evidence and granular-sync-control already this week. The boundaries confirm first, then the projection schema follows.

**Chain into `oiw-design-projection-schema` once boundaries are confirmed** — The two projection migrations (`oiw-create-observation-projection-migration` and `oiw-create-evidence-reference-migration`) both depend on a defined schema. There's no value in writing migrations that encode assumptions the schema document then contradicts. The sequence is strict here: boundary → schema → migrations, not parallel. I'd rather have the schema fully specified and only one migration written by end of day than two migrations that need revision.

**Keep the `rd100v2-fix-no-adjust-state-on-prop-change-errors` item alive** — The plan is explicit: 91 of 92 `no-adjust-state-on-prop-change` errors cleared in code, one remaining. The sprint has been running 32 days since the `2c81fa8bc4` revert established a genuine remediation baseline (not suppression). That one remaining error is worth isolating before I let the `rd100v2-state-effects-warnings-wave` item expand — 321 warnings across components is easier to read accurately when you're not second-guessing whether one unresolved error is bleeding into the warning counts. I'm honestly not sure whether that last error is a structural hooks violation or something subtle in a memoized callback, and I won't know until I look at it directly.

**Make a focused pass on `phpstan-type-shape-userworkflow-logging`** — I've been heavy on the PHPStan sprint all week and the plan is structured to keep type-shape repairs and runtime-shape repairs separated. The type-shape items in UserWorkflow and Logging (`phpstan-type-shape-userworkflow-logging`) need to land before I touch the runtime-shape items in those same domains — mixing the two strategies in a single pass produces annotation inconsistencies that require a follow-up cleanup. The baseline is at 964 PHPStan errors at level 9. The type-shape batch is where the volume is.

### Secondary Work

If the OIW boundary and schema work completes faster than expected, `oiw-run-migration-lint` is a natural next step — it's a verification gate, not an implementation item, and it's scoped to the migrations I'll have just written. No new context required.

### Maintenance

**Refresh the PHP test report** — The test health snapshot is 16 days old (0/50 passing). That's stale enough that the numbers don't reflect current state. Running `make test-fixed-batches-quick` gives me an accurate baseline and might reveal failures that are purely environmental rather than regressions. I'm not treating 0% as a crisis — I'm treating a 16-day-old snapshot as unreliable data.

**Refresh the TODO inventory** — The inventory is 15 days old per the report. Running the todo-cleanup script takes minutes and the output is useful for knowing whether any TODO comments accumulated in OIW or the PHPStan files I've been touching.

**Draft the implementation plan for `security-prod-boundary-sprint`** — 27 work units at 0% done, next item is `security-prod-boun-1831-scope`. The cryptographic tenant boundary and security sprint work share enough surface with OIW's operational observation layer that planning this now means less re-orientation when I pick it up. The domains listed (crypto-erasure, domain-auth, domain-billing, domain-infra) overlap with surfaces I've been navigating in the PHPStan remediation anyway. This is planning work, not implementation — writing the scope artifact for `security-prod-boun-1831-scope` is an hour of structured thinking, not a coding session.

**Scan Markdownlint issues in OIW planning files** — 175 issues across 11 files, and I'm about to be writing and editing files in `docs/work/planning/operational-intelligence-workspace/`. Targeted fixes in files I'm already touching is just hygiene.

### Parked

The `rd100v2-state-effects-warnings-wave` (321 State & Effects warnings) stays parked until the one remaining `no-adjust-state-on-prop-change` error is confirmed resolved. Starting the warnings sweep against an impure baseline produces noise I'd have to account for throughout the entire pass.

The `phpstan-runtime-shape-userworkflow-analytics-cdp` and `phpstan-cast-and-string-guards` items stay sequenced behind the type-shape pass — this is an ordering constraint in the remediation plan, not a deferral.

The `oiw-add-api-v1-routes` and `oiw-register-frontend-modules` items are backend-and-frontend integration work that sits downstream of the projection schema being defined. No routes to register until the projection layer exists.

<!-- plan-unit-ids: oiw-confirm-boundaries-and-source-contracts,phpstan-report-visibility-ratchet,phpstan-type-shape-mcp-etl,rd100v2-fix-no-adjust-state-on-prop-change-errors -->
<!-- SECTION: DAILY-PLAN END -->

<!-- Generated by dev-tracker build_today_plan.py -->
