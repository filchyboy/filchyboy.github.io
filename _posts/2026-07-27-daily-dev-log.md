---
layout: post
title: "Daily Dev Log - 2026-07-27"
date: 2026-07-27
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-07-27T13:47:35.529215+00:00 -->

## Today's Plan

Monday. Yesterday covered an enormous amount of ground — 152 items across thin vertical slices, test environment reliability, KPI dashboard unification, domain migration adapters, and a batch of factory tier work. None of that was on last week's plan, and that's fine. Today I'm returning to the two remediation tracks that have been running in parallel with all of it, and picking up the appointment scheduling staging work I touched yesterday.

### Main Focus

**Complete `asie-receipt-template` and move through `asie-evidence-redaction-cleanup`.** The appointment scheduling integrated staging evidence plan started two days ago and I was in it yesterday — the receipt template defines the integrated staging artifact that everything else in this plan references. Without it, the residual dispositions (`asie-bootstrap-residual-dispositions`) and the staged build admission (`asie-staging-admission-and-fixture`) are working against an undefined target. The redaction cleanup follows directly: staging evidence that hasn't been scrubbed of PII-adjacent fixture data is a compliance liability before it goes anywhere near a receipt or published disposition. These two units create the foundation the remaining four work units depend on.

**Advance `asie-journey-dependency-inventory` before touching `asie-staging-admission-and-fixture`.** The sequencing here matters more than the task descriptions suggest. Admitting a staged build without knowing the full journey and staging dependency graph means I could freeze a fixture state that's subtly incomplete — missing a service dependency or a tenant initialization that the journey assumes. The inventory is the verification step that makes the fixture trustworthy. I'm not entirely certain whether the inventory needs to be exhaustive or whether a boundary-scoped pass covering the five scheduled dispositions is sufficient. That's the real decision in this unit.

**Execute `phpstan-ratchet-knowledge-cutoff-implement` — passing effective time, knowledge cutoff, and jurisdictions correctly.** I've been heads-down on the PHPStan ratchet work all week. The plan has been active for four days with only 1 of 22 units complete, and the knowledge cutoff implementation is the unit that moves the error ledger directly. The 105 level-9 errors won't shrink until I'm actually merging fixes, and this unit has concrete scope: the call sites that build the knowledge cutoff context need to receive `effectiveTime`, `knowledgeCutoff`, and `jurisdictions` as explicit arguments rather than deriving or defaulting them internally. PHPStan is flagging this because the types aren't flowing through correctly. The fix is bounded — it's a contract-propagation problem, not a redesign.

**Resolve `phpstan-ratchet-mcp-idempotency-spike`.** I've been carrying this one for a few days without executing it. The spike question is where the idempotency contract boundary lives in the MCP domain-transfer flow — at the action class, or at the transport layer. My current thinking is the action class, because the transport layer doesn't have enough semantic context to construct a meaningful idempotency key for domain-transfer operations specifically. But I want to verify that before writing it down as settled, because if the transport layer already has a deduplication mechanism I'm not aware of, wiring up a second one at the action class would be redundant and potentially inconsistent. The spike surfaces that answer; the implement unit follows once it's resolved.

### Secondary Work

**Start `asie-bootstrap-residual-dispositions` if the receipt template and inventory land cleanly.** The five-class residual dispositions are the publishable output of this staging evidence cycle. If the earlier units close out and the receipt template is solid, there's no reason to leave this staged in the queue — it's the item in this plan with the most external visibility.

### Maintenance

**Regenerate the route health report.** It's 30 days old. `make sync-routes` against a 3,447-route surface that's been actively modified across the thin slice work is probably going to surface drift. This is a five-minute command with potentially significant diagnostic value given how many SPA mount and admin route slices landed last week.

**Draft the implementation plan for `imperative-to-declarative-refactors`.** Thirteen units, zero done, and the next item is `idr-13-current-safety-characterization`. The domain tags span a11y, analytics, backend, and collection-pipeline — that's a wide surface. Before I start executing units here, I want a clearer picture of which units are genuinely independent versus which ones share characterization scaffolding. Writing that plan now costs less than discovering mid-execution that units 3 and 7 need the same characterization harness I discarded after unit 3.

**Review `quality-debt-bootstrap-artifacts`.** This planning directory is scaffolded but has no description yet. Before it sits another week as a mystery, I should open it and either write the description or decide it's already been superseded by other work and archive it.

**Scan the 441 PHP test failures for any trivial fixture regressions.** The pass rate is sitting at 80% (1,840 of 2,333 passing, last refreshed yesterday). Given that the appointment scheduling factory tier 4 work landed yesterday, there's a real chance some of those failures are fixture-state mismatches that the new factory tier introduced rather than deep logic failures. Worth a ten-minute triage before assuming they're all hard problems.

### Parked

The `rd100v2-state-effects-warnings-wave` unit — clearing the remaining 321 State & Effects warnings outside the Phase 1 hotspots — is parked today. The appointment scheduling staging work and the PHPStan implementation units are both at earlier structural gates. Starting a warning-remediation sweep while those gates are open creates churn: if the PHPStan fixes touch files that also carry React warnings, I'd want to address both surfaces in the same pass rather than touching the same files twice. Once the staging evidence cycle and the idempotency spike are closed, the sequencing for rd100v2 is cleaner.

The `jest-coverage-report-ratchet-remediation` plan is also parked for today. The `jestcov-batch-preflight` unit is the right entry point, but I need a session without competing remediation work to do the preflight reconciliation properly — verifying the coverage report, ledger, and scheduled-run state against each other is the kind of task that produces wrong conclusions when done in parallel with active code changes.

<!-- plan-unit-ids: asie-receipt-template,phpstan-ratchet-knowledge-cutoff-spike,phpstan-ratchet-principal-key-narrow,phpstan-ratchet-scope-audit-key,rd100v2-state-effects-warnings-wave -->
<!-- SECTION: DAILY-PLAN END -->

<!-- Generated by dev-tracker build_today_plan.py -->
