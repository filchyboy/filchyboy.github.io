---
layout: post
title: "Daily Dev Log - 2026-06-29"
date: 2026-06-29
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-06-29T12:09:28.471973+00:00 -->

## Today's Plan

Monday. The react-doctor sprint and PHPStan remediation both got touches yesterday — the two items that became unplanned work (`rd100v2-fix-no-adjust-state-on-prop-change-errors` and `rd100v2-state-effects-warnings-wave`) are now the top of the in-progress list. The compute-infra plan also landed its first PR yesterday (PR #4364). Three active threads, all genuinely moving.

### Main Focus

**Clear `rd100v2-fix-no-adjust-state-on-prop-change-errors` — the last meaningful error category in the react-doctor sprint** — The plan status shows 93 errors → 1 after yesterday's pass, which means 91 of 92 `no-adjust-state-on-prop-change` errors are already cleared in code. There's one left. The root score is sitting at 74/100 with genuine remediation running (not suppression — the revert of `2c81fa8bc4` established that). Finishing this error category unblocks the State & Effects warnings wave (`rd100v2-state-effects-warnings-wave`) cleanly, and working the errors before warnings is the right order: an error-free baseline tells me which warning patterns are genuine versus which are downstream noise from the error conditions. I don't want to discover mid-warnings-sweep that an error I skipped was masking 40 warnings.

**Run `rd100v2-state-effects-warnings-wave` — 321 State & Effects warnings outside Phase 1 hotspots** — This became unplanned work yesterday, which tells me the react-doctor sprint has its own pull right now. The warnings are confirmed to be outside Phase 1 hotspots, so there's no overlap risk with already-fixed code. The 321 count is a defined target from the sprint tracker, and clearing it moves the root score materially. The sprint has been running for 30 days; I'd like to stop measuring time elapsed on it.

**Start `rcp-boundary-enums` in compute-infra** — The plan is 1 day old at 0% complete, and PR #4364 merged yesterday establishes that the branch is being actively worked. `rcp-boundary-enums` is Phase 0 — define the RCP lifecycle and provider enums before any container scaffolding happens. This is strict sequencing: `rcp-container-scaffold` can't be written without knowing what enums the container references, and the migration items (`rcp-migrations-assets-providers`, `rcp-migrations-links-collab`) depend on those enum values being stable. Getting the enums wrong at this stage is the kind of mistake that produces a second migration two weeks later to rename a column that encoded a misnamed enum variant. The planning README has the design settled: GitHub is the only active read-only provider adapter in Phase 0, which bounds the enum surface considerably.

**Continue the PHPStan remediation sweep through `phpstan-type-shape-ship-compliance`** — PHPStan is at 964 errors at level 9 per today's snapshot. The plan is 3/16 work units complete with 10 in progress. The type-shape items in Ship and Compliance are Phase 2 work, and the ordering within Phase 2 matters: type-shape repairs target property declarations and return types, while `phpstan-runtime-shape-compliance-mcp-etl` targets call sites. Running call-site repairs before property declarations are annotated produces inconsistent patterns — I fix a call site, then later fix the property declaration, and the inferred type changes in a way that invalidates the call-site annotation. I've gone through that cleanup cycle before. Type-shape first, runtime-shape second.

### Secondary Work

**Pick up `rcp-container-scaffold` if the enum work closes cleanly** — The scaffold depends directly on the enums being defined, so if `rcp-boundary-enums` finishes today, the container scaffolding is ready to start. The Phase 0 sequence is: enums → scaffold → migrations → contracts → adapters. Getting two items deep into that sequence today would be a good position heading into Tuesday.

### Maintenance

**Refresh the PHP test results** — The test report is 14 days old, which is long enough that it's not telling me anything useful about current state. The command is `make test-fixed-batches-quick`. The current snapshot shows 0/50 passing — that number is almost certainly stale rather than an accurate picture of test health, but I can't know until I run it. If the failures are environment-related, a fresh run will sort them quickly.

**Refresh the TODO inventory** — The inventory is 13 days old. The current count shows 0 items tracked, which at 32,070 files and 5,965,413 LOC is either genuinely clean or a stale report. Worth knowing which. The todo-cleanup script handles this.

**Draft the implementation plan for `security-prod-boundary-sprint`** — 27 work units at 0% done, with `security-prod-boun-1831-scope` as the next item. The domain tags (crypto-erasure, domain-auth, domain-billing, domain-infra) overlap with the provenance and cryptographic custody work that dominated last week, so the design context is reasonably current. The planning pipeline lists this as needing a tracker — getting the scope document drafted now puts it in position to start implementation this week or next.

**Check the 8 TypeScript errors in 2 files** — The ESLint snapshot is fresh today, and TypeScript is showing 8 errors across 2 files. With the react-doctor sprint actively touching frontend code, these files might already be in scope. At minimum, checking whether they're import-related takes five minutes and resolves cleanly or surfaces something worth tracking.

### Parked

**`phpstan-runtime-shape-compliance-mcp-etl` and downstream runtime-shape items** — Explicitly sequenced after the type-shape wave. Starting runtime repairs before type annotations are stable produces rework.

**`rcp-forge-provider-reader-contract`, `rcp-github-repository-metadata-adapter`, and the Phase 0 action items** — These are downstream of the scaffold, which is downstream of the enums. The sequencing is strict and I'm not skipping it.

**`context-briefing-metered-generation`** — 25 units at 0% complete and ready to start. It's not that the work isn't interesting — the metering contract is something I've been wanting to define for a while. But starting a fresh 25-unit plan while three active threads are mid-sweep would fragment the day badly. This gets its own session when the react-doctor sprint closes out.

<!-- plan-unit-ids: phpstan-report-visibility-ratchet,phpstan-type-shape-mcp-etl,rcp-container-scaffold,rd100v2-fix-no-adjust-state-on-prop-change-errors -->
<!-- SECTION: DAILY-PLAN END -->

<!-- Generated by dev-tracker build_today_plan.py -->
