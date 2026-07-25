---
layout: post
title: "Daily Dev Log - 2026-07-25"
date: 2026-07-25
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-07-25T13:46:37.969768+00:00 -->

## Today's Plan

Saturday. Yesterday's output was extraordinary in volume — the TV567–TV576 portfolio is now archived, plus a dozen horizontal slices. The board has been substantially cleared, which creates an unusual situation: the two feature sets with the strongest recent signal are both formally at 0/22 and 0/12 units complete. That's not stall — planning is done on both, and implementation is the work now.

### Main Focus

**Begin `phpstan-ratchet-test-base-concern` — scoped tenant execution in `BaseDatabaseTestCase`.** The PHPStan ratchet remediation has been the dominant technical thread across multiple days this week, and yesterday I touched it directly. The plan identifies `phpstan-ratchet-test-base-concern` as the structural prerequisite: `BaseDatabaseTestCase` is the inherited scaffold for most of the test suite, and if tenant scope resolution there is wrong, every test that extends it is silently running in a degraded context. Fixing this once at the base is categorically different from patching individual tests as each subsequent PHPStan unit surfaces the same ambient problem. The 105 PHPStan errors at level 9 don't all trace back here, but a meaningful cluster will look cleaner once the base is correct.

**Follow immediately with `phpstan-ratchet-api-tenant-route-closure`.** The scope is tight: a static closure in the tenant route setup is reaching into instance state in a way PHPStan level 9 correctly flags. The concrete fix is to identify exactly what instance members the closure depends on, extract those values before the closure boundary, and pass them in as captured variables. My uncertainty is practical rather than architectural — I want to grep the route setup for sibling closures with the same pattern before calling this done. Fixing one occurrence while leaving three identical violations in adjacent route definitions would make the ledger look better than reality is.

**Work through `phpstan-ratchet-principal-key-narrow` and `phpstan-ratchet-scope-audit-key`.** These are paired narrowing problems: authenticated privacy principal keys and tenant-scope audit deduplication values both need their types tightened to avoid mixed-type union paths that PHPStan can't statically verify. I'm sequencing these after the test base and route closure work because the principal key narrowing touches auth-adjacent code — if the base test scaffold isn't producing reliable tenant scope, any assertion I write to verify the narrowing is suspect. The audit deduplication narrowing is the lower-risk of the two, so I'll hit that first within the pair. Both units are purely type-narrowing work with no behavioral change; the risk surface is small.

**Advance `jestcov-batch-preflight`** — reconcile the coverage report, ledger, and scheduled-run state before Monday's 9 AM scheduled review. The plan has been active a couple of days with 0/12 units complete, and the preflight is explicitly the consistency gate: if the coverage ledger and the report derived from 3,818 instrumented files disagree going into the Monday pass, the batch work that follows picks up a false baseline. I'd rather spend time on this Saturday than discover the mismatch mid-batch on Monday. This is genuinely standalone from the PHPStan work, which is useful — it gives me a domain shift when I need one rather than grinding a single area for eight hours straight.

### Secondary Work

**`phpstan-ratchet-knowledge-cutoff-spike`** — if the four main PHPStan units land cleanly, this is a natural extension. The outbound-admission knowledge cutoff policy is a contract question more than a type question: what does the system actually commit to about the recency of knowledge it uses when making admission decisions? I've been wanting to dig into how that decision surface actually works. The spike doesn't produce a fix, it produces clarity, which is what `phpstan-ratchet-knowledge-cutoff-implement` needs before it can be executed correctly.

### Maintenance

**Regenerate the route health report.** It's 28 days stale. Running `make sync-routes` against 3,447 routes takes minutes and produces a current snapshot. The report was last generated before most of the horizontal slices that landed this week — the current state is unknown, which is the actual problem.

**Draft the implementation plan for `dtpr-run-contract`** — the first unit in `dev-tracker-publication-run`. This feature set is in the pipeline with 4 units unstarted, and the `build-in-public` and `dev-tracker` tags make it directly adjacent to the publication work that's an ongoing background process. The contract work here is scoped: what does a "run" actually commit to producing? Starting with that definition keeps the subsequent units from being underspecified.

**Scan for ESLint errors in files being modified today.** The ESLint report shows 0 errors and 7,265 warnings, with 5,253 flagged as fixable. I'm not running a broad sweep, but when I'm already in a file for PHPStan work, pulling up the ESLint output for that specific file and handling any warnings in scope is defensible. The PHP test pass rate is 82% (771/952 passed) — worth a targeted look at whether any of the 158 failures are in test classes that extend `BaseDatabaseTestCase`, since that's exactly the code being modified today.

### Parked

`rd100v2-state-effects-warnings-wave` (321 React State & Effects warnings) is real work but it's an isolated remediation sprint with no blocking relationship to anything I'm executing today. The PHPStan units are the more constrained resource — they're sequenced against each other, and finishing the base concern opens the principal key work, which opens the knowledge cutoff implement. I'd rather hold the React doctor sprint for a day when I have an uninterrupted stretch of frontend headspace rather than interleave it with auth and tenant-scoping work.

The `native-arm64-node-runtime` plan (11 units, `arm-node-runtime-inventory` as entry point) has been in the pipeline and I've been interested in starting it — but it's a different domain entirely and I don't have a forcing function today. That one needs a day where infrastructure context is primary rather than a secondary concern.

<!-- plan-unit-ids: jestcov-batch-preflight,phpstan-ratchet-knowledge-cutoff-spike,phpstan-ratchet-mcp-idempotency-spike,phpstan-ratchet-principal-key-narrow,rd100v2-state-effects-warnings-wave -->
<!-- SECTION: DAILY-PLAN END -->

<!-- Generated by dev-tracker build_today_plan.py -->
