---
layout: post
title: "Daily Dev Log - 2026-06-19"
date: 2026-06-19
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-06-19T13:09:36.721621+00:00 -->

## Today's Plan

Friday. Governance receipts are next in the queue after yesterday's heavy merge wave, and the PHPStan baseline work has been sitting in-progress for most of the week without closing.

### Main Focus

**Begin the governance receipts container sequence, starting with `governance-receipts-adr-boundary`** — This plan landed in "Ready to Start" status with a PR merged yesterday, which means the planning artifacts are fresh and the domain terminology is settled (Governance Receipt, Receipt Inbox, Receipt Audience Profile, Receipt Delivery Policy — all resolved as of this morning's plan update). The ADR is the right entry point because it fixes the container boundary before I create the `Core/GovernanceReceipts` skeleton. Getting the boundary wrong at this stage means the migration, the model, and the DTO all inherit that wrong boundary — and 51 tracker items is a painful scope to refactor. The governance work has been a thread running through this week's merges (alongside identity governance registry and registry governance), so the conceptual frame is already in place. The ADR defines the boundary; the skeleton follows.

**Create `governance-receipts-container-skeleton`** — Once the boundary ADR is accepted, the container skeleton is a blocking prerequisite for everything else in the plan. The migrations, model, factory, DTO, and event listener all need a container to live in. I'd rather do the ADR and skeleton back-to-back today than leave the ADR done with no implementation surface attached to it. The risk of splitting them across days is that I'll revisit the boundary decision when I start the skeleton because the ADR will feel abstract by then.

**Close out the three in-progress PHPStan items** — `phpstan-baseline-freeze-2026-06-14`, `phpstan-archive-superseded-remediation-maps`, and `phpstan-promote-harness-reference` have been actively in-progress since June 14. That's five days. The freeze is the literal foundation of the remediation plan — the `.reports/analysis/phpstan/phpstan.json` snapshot from June 14 needs to be formally committed as the baseline before Phase 2 type-shape repairs can begin in any organized way. Archiving the superseded maps and promoting the harness reference are low-complexity closures that I've been deferring while doing more visible feature work. Today is the day to stop carrying them as open items.

**Work through `governance-receipts-schema-design` and `governance-receipts-migration-receipts`** — The schema design should follow the skeleton, not precede it, because I want the container structure visible before committing to a persistence shape. The `governance_receipts` migration is the first concrete schema artifact. I'm not certain yet whether receipt delivery policies belong in a separate table with a foreign key or should be stored as a JSON column on receipts for the initial version — the `governance-receipts-migration-policies` item suggests separate tables, which is the right long-term shape, but I want to make sure the schema design artifact captures that decision explicitly rather than leaving it implicit in migration files.

### Secondary Work

**Draft the `governance-receipts-model-receipt` model and factory** — If the migrations land cleanly, the `GovernanceReceipt` model and its factory are the natural next step. The factory is important for test setup; without it, the PHPStan remediation work and test-harness items downstream have no realistic fixtures to work with.

**Advance `governance-receipts-dto-source-event`** — The `GovernanceReceiptSourceEvent` DTO defines the shape of data flowing in from TrustFabric, which determines what the `governance-receipts-listen-trustfabric` listener item needs to handle. Writing the DTO first keeps the listener implementation straightforward.

### Maintenance

**Regenerate the route health report** — The current snapshot is 7 days old, which means it predates a significant chunk of the admin route refactoring that landed this week (MFA middleware removal, publication identity API additions). 3,167 routes with a "warning" status on a week-old snapshot is not useful signal. Running the relevant make target gives me a current picture before the governance receipts routes are added.

**Regenerate PHP test results** — The 0% pass rate snapshot is 4 days old and was taken during a period of heavy refactoring. The 50 failures may well be environment-related or may have been resolved by this week's merges. I can't treat the test health as a real signal until I have a current run.

**Draft the `dev-tracker-publication-run` implementation plan, starting with `dtpr-run-contract`** — This is in the planning pipeline as a 4-unit plan at 0%, and the `build-in-public` domain tag means it's directly adjacent to the publication work I've been doing this week. The run contract defines what a publication run produces as output, which I've been circling implicitly through the publication identity and entry work that landed yesterday without formally specifying. Planning this now while the publication surface is fresh avoids reconstructing that context later.

**Check markdownlint issues against governance receipts planning artifacts** — The planning directory was updated this morning and there are 175 markdownlint issues across 11 files in the codebase. Before adding more documentation artifacts to `docs/work/planning/governance-receipts/`, it's worth running markdownlint scoped to that directory to catch formatting issues at creation time rather than accumulating them.

### Parked

**Content provenance (`cpdcp-module-interface-contract`)** — This has been recommended for three consecutive days and I've picked governance receipts over it each time. The honest reason: governance receipts have a PR that just merged, a plan that was updated this morning, and a natural entry sequence (ADR → skeleton → schema → migration). Content provenance is also at 0% with 54 units and a clear entry point, but the governance receipts boundary is more time-sensitive given the TrustFabric listener dependency. Content provenance is not blocked; it's sequenced after governance receipts gets a foundation.

**`todo-remediation`** — The p0 item (`todoremed-p0-replace-template-boilerplate`) is genuinely low-complexity but the TODO inventory report shows 0 items tracked, which means the tooling that would give me a useful picture of scope hasn't been run recently. Starting remediation without knowing the current inventory is working blind.

<!-- plan-unit-ids: cpdcp-module-interface-contract,cpdcp-pageeditor-adapter,cpdcp-takedown-intake-action,governance-receipts-adr-boundary,hubspot-conn-fe-mode-toggle,mgp-boundary-adr,phpstan-baseline-freeze-2026-06-14,todoremed-p0-replace-template-boilerplate -->
<!-- SECTION: DAILY-PLAN END -->

<!-- Generated by dev-tracker build_today_plan.py -->
