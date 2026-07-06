---
layout: post
title: "Daily Dev Log - 2026-07-06"
date: 2026-07-06
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-07-06T12:43:35.148184+00:00 -->

## Today's Plan

Monday after a heavy Sunday push — the board is significantly cleared, a batch of new horizontal slices scaffolded yesterday, and the PHPStan remediation is still the ongoing background obligation. Today is about deciding what to do with all that scaffolding.

### Main Focus

**Start `hs136-tenant-scope-classification` in the tenant isolation guardrail wave.** The plan status is confirmed: 53 non-TenantAware queued job classes found (the deep dive had estimated around 20, so the actual surface is more than twice what we expected), and 923 `withoutGlobalScope` occurrences across 432 files. The classification work — tenant-scoped versus platform-scoped models and jobs — has to happen before any enforcement changes, because the wrong classification at this stage means adding tenant scoping to infrastructure jobs that are legitimately platform-scoped. That's a harder rollback than getting the classification right first. This is the first work unit in a 9-task plan, and the tenant governance thread has been one of the week's dominant themes, so the domain reasoning is already loaded.

**Run `hs135-webhook-handler-audit` — audit idempotency posture of every webhook handler.** The evidence from yesterday's plan creation is more nuanced than the initial brief suggested: Email and Comms processors already use `IdempotencyService` from HS94's sweep, but the real gaps are the Nexmo handler, Postmark's local key builder, and the absence of a shared enforcement seam outside ETL and PaymentGateway. I want to audit the full handler inventory against that corrected picture before any of the remaining HS134/HS137 work touches related mutation paths. Knowing exactly which handlers are missing enforcement before I start touching Compliance mutation paths prevents me from accidentally closing the wrong gaps.

**Begin `phpstan-type-shape-ship-compliance` and `phpstan-type-shape-mcp-etl` from the remediation plan.** I've had heavy focus on this all week. At 990 PHPStan errors at level 9, the ordering discipline matters: type-shape repairs before runtime-shape repairs, not parallel. The reason is mechanical — fixing call sites against poorly-typed declarations just relocates errors to the next pass. Both of these items are Phase 2 work units and the right sequencing entry point given where Phase 1 left off. I've run this repair pattern enough times in this codebase to know that mixing repair categories in a single pass always generates a cleanup round I didn't plan for.

**Inventory `hs132-unmounted-surface-inventory` — built-but-unmounted compliance admin surfaces.** The plan evidence is specific: zero external importers for the DSR console components, entry-point mounting mechanism confirmed in `vite.config.ts` and `frontend/src/utils/createReactEntrypoint.tsx`. This is a pure inventory task — catalog what's built but not wired into the entry point system — and it unblocks the remaining 7 tasks in the plan. I'm genuinely curious what's sitting there; the fact that the mounting mechanism is confirmed and the components exist but aren't imported is a clean problem to characterize.

### Secondary Work

**Run `hs133-personal-data-inventory` and `hs134-retention-target-inventory` as a paired pass.** These two slices have overlapping domain territory — DSR data collection scope and retention deletion targets both require cataloging personal data sources — and the `DataDiscoveryService` source map finding (references tables with no create migrations, zero `billing_account_id` scoping) is relevant to both. The existing discovery map is suspect enough that running both inventories together is more efficient than treating them as independent. The `dueForDeletion()` method in `ConsentRetentionSchedule.php` has zero consumers outside the model; confirming the full deletion target picture while the DSR source inventory is open avoids a second traversal of the same territory.

### Maintenance

**Refresh the PHP test report.** The current snapshot is 21 days old — `make test-fixed-batches-quick` will tell me whether the 0% pass rate on 50 tests reflects a real regression or an environment drift. Three weeks of staleness on test results is enough that I genuinely don't know which of those it is right now.

**Refresh the TODO inventory.** 20 days since the last run, currently showing 0 tracked items. That number is almost certainly wrong given the volume of work that's shipped in the past three weeks. The todo-cleanup script takes minutes and the output might surface deferred items I've forgotten.

**Draft the implementation plan for `mcp-policy-decision-contract-inventory` in architecture-mcp-policy-decision-handoff.** This is the next work unit in a 4-unit plan touching agent-trust and MCP domains — areas that have been active this week. The contract inventory is the first concrete step, and drafting the plan now while the MCP architecture work from last week is recent means I don't have to reconstruct the reasoning cold later.

**Run `make sync-routes` to refresh route health.** The current report is 9 days old. 3,447 routes at a failing status — I should know whether that's an actual route-registration problem or a stale snapshot before any of the compliance surface mounting work (hs132) starts adding entry points.

### Parked

**`rd100v2-state-effects-warnings-wave`** — 321 State & Effects warnings is real work, but the compliance and tenant isolation inventories are more strategically time-sensitive right now. The warnings won't get worse by a day; the compliance surface clarity feeds into legal-hold and DSR decisions that have external dependencies.

**`hs138-retry-policy-matrix` and `hs139-commerce-baseline-count`** — Both are ready and scaffolded, but both are analytical tasks that require focused time without competing domain context. The queue retry policy matrix in particular needs the tenant-scope classification to be settled first — some of the 53 non-TenantAware queued jobs are likely also the ones without retry configuration, and I'd rather not inventory them twice from different angles.

**`security-prod-boundary-sprint`** — 27 units, none started. The plan is in the pipeline and the domain tags (crypto-erasure, domain-auth, domain-billing) are relevant to the governance thread. But starting a 27-unit sprint while 8 new horizontal slices are all at 0% is the wrong sequencing. The horizontal slices are faster to close individually and several of them feed the security picture anyway.

<!-- plan-unit-ids: hs136-tenant-scope-classification,phpstan-report-visibility-ratchet,phpstan-type-shape-ship-compliance,phpstan-type-shape-userworkflow-logging -->
<!-- SECTION: DAILY-PLAN END -->

<!-- Generated by dev-tracker build_today_plan.py -->
