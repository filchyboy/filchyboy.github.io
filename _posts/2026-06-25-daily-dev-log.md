---
layout: post
title: "Daily Dev Log - 2026-06-25"
date: 2026-06-25
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-06-25T13:50:21.350613+00:00 -->

## Today's Plan

Thursday. Yesterday was enormous — content provenance closed completely, deepsec run14 is done, boundary governance tooling landed, accessibility deferred work cleared. Eight PRs merged today alone. The codebase is genuinely cleaner than it was 48 hours ago. Now the question is what comes next, because the things sitting in "Ready to Start" are all at 0% and will stay there unless I actually start them.

### Main Focus

**Begin `gsc-confirm-existing-boundaries` in granular-sync-control** — The plan is at 0/44 work units complete and has been in planning state for a while. The first item is specifically a boundary confirmation against ADR-0300, ADR-0301, ADR-0302, and the existing `Core/IntegrationGovernance` and `Privacy/PrivacyControlPlane` containers. This step exists because the capability migration (`gsc-add-capability-migration`) can't be written until I know which container owns the new `GranularSyncCapability` model — putting it in the wrong container at migration time creates a schema cleanup problem that's harder to fix than getting the boundary right first. The planning README has already done the ADR research; I need to convert that research into a boundary confirmation artifact, then the migration and model items follow sequentially.

**Work through `rce-confirm-boundaries-source-context` in regime-compliance-evidence** — This item confirms ADR-0301 boundaries against existing privacy containers before any evidence lifecycle schema work begins. I'm looking at the same class of problem as the granular-sync boundary work: write the migration before the container boundary is confirmed, and the schema ends up in the wrong place. `rce-add-lifecycle-migration` and `rce-add-retrieval-custody-migration` are both downstream of this confirmation, so the sequencing is strict. The plan is at 0/51 tracker items — that's a lot of scope to get wrong early.

**Continue the phpstan-baseline-remediation sweep, targeting `phpstan-type-shape-ship-compliance`** — The plan is at 3/16 work units complete with 9 in progress. I've had significant focus here recently, and the type-shape findings in Ship and Compliance are Phase 2 work — the baseline freeze and archive items from Phase 1 are done, which means this is the right next layer. What I've noticed doing this kind of remediation is that "type-shape" errors in PHPStan level 9 often cluster around return type covariance in domain service boundaries, not scattered through the whole domain. If the Ship and Compliance containers follow that pattern, I might be able to address a large portion of the findings by fixing a small number of interfaces rather than patching call sites one by one. Worth checking before I start touching individual files.

**Run `tenant-trust-source-coverage-audit`** — This is the one ready item in tenant-trust, and it's a prerequisite for everything in Phase 1. The plan has been in planning state and the coverage audit establishes which evidence sources the trust framework actually covers versus which ones are assumed. I can't write the source-event listener contracts (Phase 1 proper) without knowing what sources are in scope. The audit itself is documentation and verification work — read the existing event sources, cross-reference against the trust model, produce the coverage artifact. Bounded enough that it shouldn't consume the whole day, but it has to happen before the listener contracts become actionable.

### Secondary Work

**Draft the implementation plan for `crypto-prov-integration-mutations-signing-plan`** in cryptographic-provenance-integration-mutations — This is a single-unit planning directory currently at 0/1 complete. The domain tags are cryptographic-provenance, integrations, MCP, and security, which places it squarely in the security/provenance push that's been the dominant thread this week. Having the signing plan artifact written means the mutation signing work can move to implementation-ready rather than sitting in the pipeline needing research.

### Maintenance

**Refresh the PHP test report** — The test results are 10 days stale. The pass rate is currently 0% (0/50 passed), but that number is old enough that it may not reflect recent work. Run `make test-fixed-batches-quick` to get a current picture. Ten days is long enough that the content provenance and deepsec remediation work from this week might have already fixed some of the failures — I won't know until I look.

**Refresh route health** — `make sync-routes` to regenerate the route health report. At 13 days old and 3,167 routes with a warning status, the current snapshot predates a significant amount of work. The boundary governance tooling sprint that just merged likely touched route registration; the current report doesn't reflect that.

**Refresh the codebase metrics** — `make codebase-metrics` to update the LOC and file count. Eleven days stale across an active week is a wide gap. Not urgent, but the metrics are used as a baseline reference in planning conversations and the current numbers predate multiple feature set completions.

**Check markdownlint issues in planning files being touched today** — The granular-sync-control and regime-compliance-evidence planning directories are both getting edited as part of today's boundary confirmation work. The markdownlint report shows 175 issues across 11 files. Before committing the boundary confirmation artifacts, spot-check the planning READMEs in those directories against the markdownlint rules — it's cheaper to fix them during the edit than to run a separate cleanup pass later.

### Parked

The `security-prod-boundary-sprint` (27 units, next: `security-prod-boun-1831-scope`) and `production-readiness-reconciliation` (33 units, next: `production-readine-2092-scope`) are both sizable planning-to-implementation transitions that deserve dedicated time. I'm not touching either today because the boundary confirmation work in granular-sync and regime-compliance-evidence needs to close first — those three feature sets share the ADR-0301 space, and I'd rather not have two overlapping boundary discussions running simultaneously. The security sprint also starts with a scope item, which is the kind of work that expands if you give it time next to open boundary questions.

The `phpstan-cast-and-string-guards` and `phpstan-database-factory-model-wave` items are in the remediation tracker but lower priority than the type-shape work. The type-shape findings tend to be the highest-density problem in level 9 runs, so clearing Ship/Compliance and MCP/ETL first gives me a better picture of what remains before I move to casts and database patterns.

<!-- plan-unit-ids: gsc-confirm-existing-boundaries,phpstan-report-visibility-ratchet,phpstan-type-shape-ship-compliance,phpstan-type-shape-userworkflow-logging -->
<!-- SECTION: DAILY-PLAN END -->

<!-- Generated by dev-tracker build_today_plan.py -->
