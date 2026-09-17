---
layout: post
title: "Daily Dev Log - 2026-09-17"
date: 2026-09-17
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-09-17T16:08:04.126713+00:00 -->

## Today's Plan

The MySQL contention proofs are all progressed but not closed, the admission inventory allocation items landed unplanned yesterday and want a contract review, and the thin-vslice baseline queue has four items I touched yesterday that are ready to move.

### Main Focus

**Close the five MySQL contention proof items in `appointment-scheduling-productization`** — All five (`asp-01-prove-mysql-workflow-contention`, `asp-01-prove-mysql-public-hold-contention`, `asp-01-prove-mysql-confirmation-contention`, `asp-01-prove-mysql-dispatch-contention`, `asp-01-prove-mysql-refund-contention`) are progressed but not done. These aren't independent tests — they're a suite, and the dispatch contention proof specifically gates the stale-result fencing logic in `asp-01-fence-appointment-dispatch-claim-results`. I can't close the fencing item with confidence until I have a real contention scenario demonstrating the race condition it's supposed to prevent. The sequencing here is strict: prove the contention exists, then verify the fence holds. Getting all five proofs to a closed state today would unblock the fencing work cleanly.

**Complete `admission-contract` in `admission-inventory-allocation`** — The five implementation items (`admission-ga-config-request`, `admission-ga-config-policy`, `admission-ga-schema`, `admission-ga-model`, `admission-ga-config-action`) all landed yesterday as unplanned work. That's the full configuration mutation stack — request validation, policy authorization, migration, model, and the action itself. The one remaining item is the P03 contract reconciliation (`admission-contract`). The plan's stated deliverable is the reviewed contract, not the implementation, so closing the implementation without closing the contract review leaves the plan in an awkward half-finished state. The contract reconciliation is where I verify the implementation actually matches the contract shape — I want to do that while the implementation choices are fresh.

**Review `service-rights-f01` in `service-entitlement-ledger`** — This has had heavy focus all week and was touched yesterday. The work unit is "Issue and evaluate acquired service-use rights" — the F01 implementation that the events-scheduling sequence depends on. ADR-0371 and the service-use contract in `docs/architecture/contracts/service-use-rights.md` define the Commerce/ServiceEntitlements selection, so the design is settled. What I'm checking is whether the issuance and evaluation implementation is coherent with the entitlement boundaries the contract specifies. I haven't verified those edges explicitly, and this is the kind of thing that's easier to catch before any downstream feature set starts consuming the ledger.

**Advance `venue-contract` in `venue-space-holds`** — Active all week and touched yesterday. This is a P03 contract review, same structure as `admission-contract`. The venue-space-holds plan is independent of admission-inventory-allocation — they share the broader events-scheduling sequence but carry separate ownership. The contract review here involves reconciling the room reservation semantics from `thin-vslice-747` (an event operator reserves a non-staff resource through Calendar's occupied-time authority) against the venue contract boundaries. I've been deferring this for a couple days in favor of implementation work; I want to spend real time on it today rather than letting it continue to slide.

### Secondary Work

**Start `tv755-contract-scope-baseline` for the event-wide cancellation slice** — This is ready to start and I touched it yesterday. The scope baseline for event cancellation needs to capture the cancellation boundary: one event instance, confirmed paid/free attendees, booking/refund/resource/notification impact preview, then a single commit with no duplicate refunds and no orphaned occupied-time reservations. The interesting constraint is the atomicity requirement — the slice has to be designed so that partial execution still leaves a recoverable state. I want to at least get the contract document structured before I move off the scheduling domain for the day.

**Draft an implementation plan for `events-scheduling-competitive-intelligence`** — This is in the planning pipeline and aligned with the scheduling work I'm already doing. Two artifacts exist (`activation-budget-expense-unit-economics-pass.md` and `event-trust-safety-integrity-pass.md`), so there's prior research to build from. The plan needs a tracker and scope document. Given how much scheduling work is in motion right now, getting this planned while I'm oriented in the domain reduces future ramp-up.

### Maintenance

**Run `make sync-routes`** — Route health was last checked 82 days ago. 3,447 routes and a failing status is a wide gap to leave unverified, especially with the appointment scheduling and admission work adding new endpoints. I'm not expecting a crisis, but an 82-day-old snapshot is genuinely not useful for anything.

**Run `make test-fixed-batches-quick`** — The PHP test results are 49 days old, showing 0% pass rate against 1,583 tests. That number almost certainly reflects an environment issue rather than 1,583 regressions, but I won't know until I run it. The contention proof work I'm doing today is inherently test-adjacent — good moment to get a fresh test report alongside the contention scenarios.

**Check Markdownlint against files in `docs/work/planning/appointment-scheduling-productization/`** — 61 Markdownlint issues across 4 files. I'm editing planning documents in this directory today anyway. Addressing the issues file-by-file rather than with a blanket fix command means I can spot any that are genuine content problems versus formatting noise.

**Run `make codebase-metrics`** — 57 days stale. Not urgent, but the codebase is at 39,121 files and growing. Keeping metrics fresh costs almost nothing and having a current LOC baseline is useful context for the blog posts where I write about scale.

### Parked

**`events-scheduling-shared-contracts` P02 items** — The five contract and authority items (`p02-source-audit`, `p02-rights-contract`, `p02-authority-contract`, `p02-hierarchy-credentials`, `p02-review-admission`) have been active this week but I'm not touching them today. The P03 contract reviews for venue and admission need to close first — trying to work P02 and P03 simultaneously on the same sequence creates reconciliation noise. P02 can return once the P03 owners are stable.

**`agent-runtime-quiescence`** — Thirteen items in motion, zero recent activity. The `arq-owner-review-and-merge` item is explicitly blocked. The rest of the queue is valid work, but with the scheduling and admission contracts demanding attention today, dropping into a completely separate domain here would split my focus too thinly. The quiescence work will surface again when the scheduling arc closes out a phase.

**The thin-vslice baselines for tv719, tv667, tv721, and tv725** — All active this week and ready to start, but each needs a focused sitting to get the scope baseline right. Doing contract baselines for four separate slices in the same day tends to produce shallow documents. I'll return to these once the two I'm prioritizing (tv755 and the secondary work above) are in better shape.

<!-- plan-unit-ids: admission-contract,asp-01-fence-appointment-dispatch-claim-results,asp-01-preserve-notice-authority-across-unrelated-revisions,asp-01-require-google-event-lookup-evidence,p02-source-audit,venue-contract -->
<!-- SECTION: DAILY-PLAN END -->

<!-- Generated by dev-tracker build_today_plan.py -->
