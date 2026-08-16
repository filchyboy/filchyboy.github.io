---
layout: post
title: "Daily Dev Log - 2026-08-16"
date: 2026-08-16
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-08-16T13:03:21.358330+00:00 -->

## Today's Plan

Sunday. The Shopify ETL foundation shipped yesterday — that whole feature set is archived — and the appointment scheduling productization work has 20 items in motion from yesterday's session. Today is about deciding how much further I take the ASP work before switching gears, and whether the staging evidence sprint finally closes.

### Main Focus

**Close out the `asie-evidence-redaction-cleanup` and `asie-bootstrap-residual-dispositions` items** — The `appointment-scheduling-integrated-staging-evidence` plan has been open for 21 days. Those two remaining items are verification and publication work, not design work — they're the last gate before this plan archives. The residual dispositions artifact feeds directly into the productization phase's published guides, so leaving it incomplete creates a gap in the ASP handoff chain. I want this plan closed today.

**ASP Phase 01 completion push on the `asp-01-*` items** — All 20 Phase 01 work units are currently in progress from yesterday's session. The items span the full booking lifecycle: governed link persistence, slot hold atomicity, commerce quote composition, cancellation/refund execution, and the tenant isolation proof. I'm not going to try to close all 20 — the goal is to pick the ones where the implementation decision is already settled and there's nothing blocking execution, versus the ones that genuinely need a design pass. The `asp-01-reconcile-public-booking-contracts-with-adrs-0340-through` item is the anchor: if the ADR reconciliation is solid, the downstream items (authorization discovery, cross-tenant concealment, operation-bound grant policies) follow in a clear sequence. I'll start there and work down the dependency chain.

**`shopify-estate-foundation-admission`** — The Shopify synthetic acceptance estate plan is blocked on production-grade foundation admission. That admission gate is exactly what shipped yesterday (`shopify-foundation-admission-gate`). So the estate plan may have just become unblocked, which means `shopify-estate-foundation-admission` is the verification step that confirms it. This is the kind of thing I need to check before the plan accumulates more false-blocked time.

**Market intelligence Stage 2 corpus work** — `mi-stage-2-company-investor-corpus` and `mi-stage-2-customer-corpus` have been on the plan for two days. I'll be honest: the collection work is slower than I want it to be, partly because the source pool for the investor corpus and the customer/community corpus don't overlap much, so I can't batch them efficiently. The corpus currently has 78 sources and 67 evidence records. I need to actually close the collection loops on both tracks, not add more scaffolding around them.

### Secondary Work

**ASP Phase 02 readiness check** — With Phase 01 items progressing, the five Phase 02 ready-to-start items are worth a brief review: `asp-02-specify-tenant-merchant-account-capability-and-lifecycle-c`, the merchant onboarding runbook, and the funds-flow conformance evidence. I won't begin implementation today, but I want to know whether Phase 02 has any dependency on Phase 01 items that aren't resolved yet. If the merchant account capability spec can start independently, I'd rather know that now than discover it Monday.

### Maintenance

**Refresh the PHP test report** — The test results are 17 days old. Running `make test-fixed-batches-quick` takes a session and produces a fresh baseline. I have no idea whether the current 0% pass rate reflects the actual state or just an environment issue from two weeks ago. A fresh run either confirms a real problem worth addressing or retires the stale number.

**Refresh route health** — Route health is 50 days old. `make sync-routes` is the command. With 3,447 routes tracked and significant feature work landing over the past seven weeks, the stale report is almost certainly wrong about current state. This takes minimal time and removes a data quality gap.

**Markdownlint on the ASP planning docs** — There are 61 markdownlint issues across 4 files. I'll be touching the ASP planning directory today for the Phase 01 reconciliation work anyway. Running markdownlint scoped to `docs/work/planning/appointment-scheduling-productization/` will surface any issues in files I'm already editing, so I can fix them in the same commit rather than as separate cleanup.

**Draft the implementation plan for `jest-coverage-report-ratchet-remediation`** — This is in the planning pipeline with 12 work units and zero done, tagged with a11y, api, authorization, and audit scope. The next item is `jestcov-batch-preflight`. Drafting the implementation plan is a planning task, not a code task — it's well-suited to the end of a Sunday when the implementation energy runs low. The jest coverage work is also adjacent to the 6,648 ESLint warnings; getting the ratchet remediation structured now means I have a real plan for the warning backlog rather than a vague intention.

### Parked

**`react-doctor-100-followup-sprint-v2`** — The 321 remaining State & Effects warnings have no dependency on today's work and clearing them is a focused remediation session, not something to start mid-ASP. Parked until the ASP phase work settles.

**`deepsec-run14-external-evidence-follow-up`** — Five work units, none started. The first is a source reconciliation task, and I don't want to context-switch into security evidence gathering while the ASP items are mid-stream. This waits.

**`documentation-hierarchy-audit-remediation`** — Ten work units starting at `dha-054-email-cdp-cutover-metadata-lint`. Legitimate work, but it competes with the ASP documentation effort and I'd rather close the ASP docs first so I'm not editing overlapping artifacts simultaneously.

<!-- plan-unit-ids: asp-01-reconcile-public-booking-contracts-with-adrs-0340-through,dha-052-auth-waiver-frontmatter,dha-054-email-cdp-cutover-metadata-lint,mi-stage-2-company-investor-corpus,shopify-estate-foundation-admission -->
<!-- SECTION: DAILY-PLAN END -->

<!-- Generated by dev-tracker build_today_plan.py -->
