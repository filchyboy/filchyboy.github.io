---
layout: post
title: "Daily Dev Log - 2026-07-24"
date: 2026-07-24
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-07-24T14:10:22.972480+00:00 -->

## Today's Plan

Friday, and the PHPStan work that's been the backbone of this week is finally meeting its implementation gate — the ratchet remediation plan is ready to start and I worked on it yesterday.

### Main Focus

**Begin implementation on `phpstan-ratchet-test-base-concern` — adopting scoped tenant execution in `BaseDatabaseTestCase`.** The `phpstan-report-ratchet-remediation` plan is 0/22 units complete with planning finished, and `phpstan-ratchet-test-base-concern` is listed as the natural entry point. The reason to start here rather than with one of the more semantically interesting units like `phpstan-ratchet-knowledge-cutoff-spike` is structural: `BaseDatabaseTestCase` is the test scaffold that most other tests inherit from. If the scoped tenant execution pattern isn't right at that base, the subsequent unit-by-unit repairs are each fighting the same ambient problem. I'd rather fix the floor once than patch around it ten times.

**Work through `phpstan-ratchet-api-tenant-route-closure` — removing instance access from the static tenant route closure.** This one is genuinely tidy in scope: a closure that shouldn't be reaching into instance state. The bug class is well-understood — a static closure capturing `$this` (or effectively doing so through a variable) is a PHP runtime risk and a PHPStan level-9 flag. The fix is a bounded refactor: identify what the closure actually needs from the instance, extract it before the closure boundary, and pass it in explicitly. No architectural ambiguity. My only uncertainty is whether the tenant route setup has other closures with the same pattern that aren't yet in the ledger — that's worth a quick grep before committing the fix so I'm not creating a false sense of completeness.

**Advance `phpstan-ratchet-principal-key-narrow` and `phpstan-ratchet-scope-audit-key`.** These two units are about narrowing key types — authenticated privacy principal keys and tenant-scope audit deduplication values. They're paired in the plan and the remediation work on both is the same shape: PHPStan is seeing a wider union type than what the runtime actually produces at the call site, and the fix is adding an assertion or narrowing the declaration. I want to tackle both together because the audit deduplication key type is downstream of the principal key in the authorization flow — if I narrow the principal key correctly, the audit key type might resolve without a separate change. Worth verifying before writing two independent fixes.

**Start `jestcov-batch-preflight` for the Jest coverage ratchet.** The scheduled review runs Monday, Wednesday, and Friday at 9 AM Pacific. Today is Friday, which means if the preflight reconciliation isn't clean before this morning's window, the scheduled pass picks up an inconsistent baseline. The plan has 3,818 instrumented files from the current worktree; the preflight unit is the reconciliation step between the coverage report, the ledger, and the scheduled-run state. This isn't complicated work, but it's time-sensitive in a way the PHPStan units aren't — letting it slip to Monday means the next two scheduled runs (Monday and Wednesday) are also starting from an unverified baseline.

### Secondary Work

**Advance `phpstan-ratchet-mcp-idempotency-spike` — resolving the MCP domain-transfer idempotency contract.** This is a spike unit, which means it's explicitly scoped as investigation rather than implementation. The question it's answering is what the correct idempotency contract looks like for MCP domain transfers when the same transfer is retried. That question needs answering before the corresponding PHPStan type narrowing can be written correctly — the type shape of the return value depends on whether domain-transfer is idempotent at the operation level or only at the data level. Worth a pass today if the main PHPStan units finish early, because the spike output feeds directly into subsequent implementation units.

### Maintenance

**Run `make sync-routes` to refresh the route health report.** The current snapshot is 27 days old and covers 3,447 routes. Route health should be refreshed regularly and nearly a month is too long to let it drift, especially during a week where multiple vertical slices have landed and modified API surface. This is a single command with a deterministic output — no reason to defer it.

**Draft the implementation plan for `phpstan-baseline-remediation → phpstan-type-shape-ship-compliance`.** The baseline remediation plan is 40 days old with Phase 2 (high-volume type-shape repairs) in planned status. I've been heads-down on the baseline work all week, and the Ship/Compliance type-shape surface is the logical next wave. While I have the PHPStan error taxonomy fresh from the ratchet work, I should sketch the scope and ordering for the Ship/Compliance pass — specifically which files have overlapping type-shape and guardrail violations so I can sequence them correctly. That sketch belongs in the planning artifact, not just in my head.

**Scan for PHPStan-flagged files being modified in today's ratchet work and check ESLint warnings in the same surfaces.** The ESLint warning count is 7,323 (5,270 fixable), and the route closures and tenant-scoped base classes I'm touching in the ratchet work are likely to have overlapping JS/TS surface if they have frontend counterparts. I'm not running a broad fix pass — just checking whether the specific files in scope today carry warnings I can address with targeted edits while I'm already there.

### Parked

`phpstan-baseline-remediation` phases 2–5 are not today's target. The ratchet remediation is the active gate: 35 findings across ten root causes need to clear through the ratchet plan before I return to the broader baseline wave. Running both concurrently would muddy the attribution — a finding that drops from the report could be from either effort, and I'd lose the ability to verify each ratchet unit's impact cleanly.

The `react-doctor-100-followup-sprint-v2` work (321 State & Effects warnings to clear) is parked until the PHPStan surface is further along. The ESLint warning count is already documented and the eslint-report-ratchet-remediation plan just archived — I want one ratchet track active at a time.

`native-arm64-node-runtime` is not today's priority. The inventory unit (`arm-node-runtime-inventory`) is the correct entry point and I worked on it yesterday, but the Friday schedule is better spent closing the PHPStan ratchet units that have a direct relationship to test infrastructure I'll be touching anyway in `phpstan-ratchet-test-base-concern`.

<!-- plan-unit-ids: phpstan-ratchet-test-base-concern,phpstan-report-visibility-ratchet,phpstan-type-shape-mcp-etl,phpstan-type-shape-userworkflow-logging -->
<!-- SECTION: DAILY-PLAN END -->

<!-- Generated by dev-tracker build_today_plan.py -->
