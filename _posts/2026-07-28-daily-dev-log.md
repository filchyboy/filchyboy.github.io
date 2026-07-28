---
layout: post
title: "Daily Dev Log - 2026-07-28"
date: 2026-07-28
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-07-28T14:07:26.396971+00:00 -->

## Today's Plan

Tuesday's focus is moving the appointment scheduling staging evidence plan through its execution sequence while keeping the documentation remediation work from stalling on its first day.

### Main Focus

**Run through `asie-booking-payment-confirmation` → `asie-reviewed-receipt-closeout` → `asie-staging-admission-and-fixture`.** I was in this plan yesterday and the sequencing is load-bearing. The booking, availability, payment, and confirmation observation (`asie-booking-payment-confirmation`) produces the raw evidence that the receipt closeout depends on — there's no useful receipt to review if the booking flow evidence hasn't been captured. That observation feeds `asie-reviewed-receipt-closeout`, which is the gate before I can do anything meaningful with `asie-staging-admission-and-fixture`. Admitting the staged build and two-account fixture against an unreviewed receipt creates an ambiguity about what the fixture is supposed to validate. The order isn't advisory, it's structural. I've been in this plan for two days and the remaining five units are all in the ready queue — today I want to get through at least three of them.

**Advance `asie-bootstrap-residual-dispositions` and `asie-evidence-redaction-cleanup` after the receipt is reviewed.** The five-class residual dispositions can't be published until the staged build is admitted and the fixture is verified — they reference the fixture state. The redaction cleanup is the compliance-adjacent step: any staging evidence that carries PII-adjacent fixture data needs to be scrubbed before it becomes part of the published receipt record. I'm not entirely certain whether the redaction pass needs to cover the booking observation evidence captured in `asie-booking-payment-confirmation` or only the fixture artifacts from `asie-staging-admission-and-fixture`. That's the real judgment call in the cleanup unit, and I'd rather verify the scope there than assume and miss something.

**Execute `dha-054-email-cdp-cutover-metadata-lint` from the documentation hierarchy audit remediation.** This plan started today and is at 0/10 units — `dha-054` is the natural entry point. The email contacts CDP cutover documentation has metadata drift and markdownlint violations that are contributing directly to the two current markdownlint issues showing in the lint report. Fixing the metadata and resolving the lint violations in those specific files is a clean, bounded first execution in a plan that otherwise has ten units ahead of it. The markdownlint report shows 2 issues across 1 file — this is likely the file. Getting it clean on day one of the plan establishes the baseline the health gates need.

**Implement `phpstan-ratchet-knowledge-cutoff-implement` — pass effective time, knowledge cutoff, and jurisdictions correctly.** This has been active all week and I touched it a couple of days ago. The PHPStan baseline is at 14 errors at level 9, and this specific unit addresses the contract around how temporal and jurisdictional context flows through to PHPStan-visible call sites. The risk I'm trying to avoid is implementing the parameter passing correctly in isolation while leaving callers that pass stub values or nulls — PHPStan level 9 will surface that immediately, but I'd rather audit the call graph before the commit than discover it in CI. What I don't yet know is whether the knowledge cutoff value is expected to be passed as a typed value object or a primitive timestamp; the contract baseline work from earlier in the plan should settle that, but I'll verify before writing the implementation.

### Secondary Work

**Convert `dha-052-auth-waiver-frontmatter` metadata to frontmatter.** This is the second ready unit in the documentation hierarchy audit remediation. If `dha-054` closes cleanly, this is the natural follow-on — the auth security waiver document is a different metadata pattern but the same structural problem. Converting ad-hoc metadata representations to proper frontmatter across the documentation hierarchy is the work the entire plan is built around; doing two units in sequence on the first day of the plan would be a solid start.

### Maintenance

**Run `make sync-routes` to refresh the route health report.** The report is 31 days old. It covers 3,447 routes and its current status is `fail`, but I genuinely can't tell whether that failure is a real routing problem or just drift from the last sync — the report is too stale to trust either way. This is a single command that produces a refreshed snapshot. I should know what the route graph looks like.

**Draft the implementation plan for `jest-coverage-report-ratchet-remediation`.** The pipeline shows 12 units ready with `jestcov-batch-preflight` as the next step. This is aligned with the quality remediation work I've been doing across PHPStan and markdownlint — getting the Jest coverage ratchet plan to a startable state while PHPStan is mid-execution means I'm not blocked when the PHPStan work clears. The plan needs a `tracker.json` pass to confirm the unit sequencing before I touch it.

**Resolve the `rd100v2-state-effects-warnings-wave` unit in `react-doctor-100-followup-sprint-v2`.** The ESLint report shows 6,873 warnings with 5,203 marked fixable. The State & Effects warnings (321 of them) outside the Phase 1 hotspots are what this unit targets. I'm not going to run a broad auto-fix pass — the repo's history with that is that it generates noise requiring cleanup. Instead, I'll scope this to the specific files that the Phase 1 hotspot list already identified as boundary-adjacent and address the warnings there manually. Whether 321 warnings reduces meaningfully from a targeted pass is an open question, but at minimum it narrows the surface.

### Parked

The `quality-debt-bootstrap-artifacts` planning directory needs investigation before anything can be scheduled from it — there's no description and no units yet. I'm not touching it today; the research pass belongs in a planning session, not a Tuesday execution day.

The `deepsec-run14-external-evidence-follow-up` and `test-harness-ci-manifest` plans are both in the pipeline with zero units done. Neither is blocking today's work, and pulling them into focus while the appointment scheduling evidence sequence is mid-execution would create context-switching costs I don't want. They'll surface again when the staging evidence plan closes.

<!-- plan-unit-ids: asie-staging-admission-and-fixture,dha-050-phpstan-harness-plan-link,dha-052-auth-waiver-frontmatter,dha-054-email-cdp-cutover-metadata-lint,rd100v2-state-effects-warnings-wave -->
<!-- SECTION: DAILY-PLAN END -->

<!-- Generated by dev-tracker build_today_plan.py -->
