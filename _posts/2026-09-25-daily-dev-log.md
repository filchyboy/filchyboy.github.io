---
layout: post
title: "Daily Dev Log - 2026-09-25"
date: 2026-09-25
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-09-25T13:52:42.849688+00:00 -->

## Today's Plan

Friday. The demo is behind me, the audit trails are closing, and privacy-category-management is where the real construction work sits now.

### Main Focus

**Drive `col-6038-scheme-model` and `col-6038-definition-model` to closed state** — These two models are the structural core of everything upstream in the COL-6038 branch. `PrivacyCategoryScheme` and `PrivacyCategoryDefinitionVersion` are prerequisites for the migration items, the relationship persistence, the digest canonicalization — essentially everything in the 44-item in-progress list touches one of these. I progressed both yesterday but neither closed. The risk of leaving model definitions in an intermediate state over a weekend is that I lose the precise design reasoning that exists right now. The `col-6038-governance-adr` I finished yesterday documents the ownership decision, so the design is settled — execution is what's left.

**Close `col-6038-category-canonical-digest`** — The canonicalization of semantic and presentation digests is a correctness boundary, not just an implementation detail. If the digest function isn't deterministic across the same category definition, every downstream comparison (`col-6038-catalog-compare`) and export (`col-6038-catalog-export`) will produce inconsistent results. I want this resolved before I touch any of the comparison or export logic — fixing a flawed digest contract after those are built is significantly more expensive than getting it right now. This is strict sequencing, not preference.

**Work through `col-6038-determination-digest` and `col-6038-determination-clone`** — Both are in Ready to Start, which means their prerequisites are satisfied. The determination digest canonicalization parallels the category digest work above and should be done in the same session while the design reasoning is consistent. The clone item — immutable determination successors — is the mutation pattern that `col-6038-governed-mutation-task` depends on. Getting these two closed today means the governance mutation path unblocks on Monday rather than mid-next-week.

**Advance `w4-effect-containment` and `w1-request-provenance` in the synthetic-scenario-actor-audit** — I progressed both yesterday but the containment proof in `w4-effect-containment` isn't done and `w1-request-provenance` still needs the origin trail resolved. The provenance matrix is a gate on `w3-scenario-owner-fidelity` — the actor fidelity binding can't be credibly claimed until the request origin trail is established. I got `w5-effective-identity` into yesterday's unplanned work, which is useful context for the effective-identity boundary design, but the containment proof is more urgent: the demo disposition artifact in `artifacts/demo-disposition.md` cannot produce removal decisions until `w4-effect-containment` has its proof. These two items are the ones that need to close this week, not next.

### Secondary Work

**Draft an implementation plan for `pr-stack-reconciliation-20260906`** — This is flagged as aligned with active privacy-category-management work. The PR stack reconciliation shares the same domain I've been building in all week, and the planning directory needs concrete next steps rather than just scaffolding. With the COL-6038 branch already taking shape, this is the right moment to document what the stack looks like and what order the PRs need to merge.

**Start `col-6038-archival-command`** — This is in Ready to Start and has a clear behavioral boundary: block archival when active consumers exist. The `col-6038-inventory-consumers` item I progressed yesterday gives me the consumer map I need to write the archival guard correctly. These two items are directly connected, and the inventory work is still fresh enough that writing the guard today costs less than reconstructing context next week.

### Maintenance

**Regenerate PHP test results with `make test-fixed-batches-quick`** — The test report is 57 days old. That's not a healthy gap for a codebase this size. The 0% pass rate almost certainly reflects environment state rather than 1,583 genuine regressions, but I won't know until I run it. I'm not going to make decisions about test health against a 57-day-old snapshot.

**Refresh TODO inventory with the todo-cleanup script** — 65 days since the last inventory. With the amount of work that's landed recently — agent-runtime-quiescence, synthetic-scenario, the entire cvg series — there are almost certainly resolved TODOs that are still tracked and new ones that aren't. This is a 10-minute task that keeps the inventory meaningful.

**Check the 3 TypeScript errors in the one affected file** — ESLint is clean on errors but TypeScript is reporting 3 errors in a single file. Given that `col-6038-frontend-api-client` is on the work list, I want to know if the TypeScript errors are in that file or adjacent to it before I start adding typed API surface. Missing type imports are the most likely cause and the most straightforward fix.

**Review Markdownlint issues in planning docs being touched today** — 61 issues across 4 files. The privacy-category-management planning directory is active right now, and if any of those 4 files are the ones I'm writing to today, I should clear the issues in the same edit pass rather than accumulating them.

### Parked

**`admission-inventory-allocation`**, **`external-event-graph-consumption`**, and **`events-scheduling-shared-contracts`** haven't been touched recently and aren't blocked — they're just lower priority than closing out active COL-6038 construction work. The admission contract and venue contract items each need their respective P03 contract reconciliation work, which is a different kind of effort than what I'm doing today.

**`rd100v2-state-effects-warnings-wave`** — 321 ESLint State & Effects warnings is real work, but it's not the kind of work to start on a Friday afternoon alongside active model implementation. This needs a focused session with no competing construction work in the same area.

**`scheduling-surface-parity-audit`** and **`campaign-scenario-adapter`** are flagged as needing research. Both are genuine planning tasks but the research phase requires a different mental posture than the implementation work I'm doing today, and I don't want to split attention between COL-6038 model construction and audit research.

<!-- plan-unit-ids: admission-ga-writer-audit,col-6038-inventory-consumers,col-6038-registry-manifest,col-6038-scheme-migration,p02-source-audit,w2-synthetic-demo-inventory -->
<!-- SECTION: DAILY-PLAN END -->


<!-- SECTION: ACCOMPLISHED START -->
<!-- accomplished-generated: 2026-09-25T19:56:28.420683+00:00 -->

## Today's Update

Today was CVG-010 from end to end. Twenty-three work units across capability consumption controls, closed out in sequence — from scoping through implementation, testing, UI, and archive. That's an unusual shape for a day; normally I'm threading between three or four feature areas rather than driving one feature set to completion. The payoff is that CVG-010 is done and reconciled, not just "mostly there."

The architectural core of CVG-010 is a spend control boundary that governs how capabilities are admitted and how budget transfers are reserved before anything is consumed. I defined that boundary explicitly (`cvg010-04`) and traced every reserve and admit caller (`cvg010-03`) before touching implementation — the call-site inventory is the kind of thing that saves you from a silent bypass later when a new service import path goes in without a guard. From there the serialization work built outward: ordinary budget admission (`cvg010-06`), transfer window reservation (`cvg010-07`), and the settle/release replay path (`cvg010-08`), each with immutable request binding so that replay operations can't mutate the original intent mid-flight. The attribution layer (`cvg010-09`) ties capability and transfer records back to the actor that originated them, which is what makes consequence preview (`cvg010-10`) meaningful — if attribution is missing, the preview surface is just showing aggregate math with no accountability chain attached to it. The time-bound transfer exception (`cvg010-11`) was a deliberate narrowing: rather than making all transfers potentially exception-eligible, I scoped the exception path to a specific window condition, which keeps the guard logic in `cvg010-12` from needing to reason about open-ended eligibility. Proving competing admissions on MySQL (`cvg010-13`) was the test I was least confident about before running it — concurrent admission races are exactly the kind of thing that passes on an unloaded test database and fails under contention. It held.

The UI side of CVG-010 centers on `SpendControlCenter`, which I extended with transfer scope (`cvg010-15`) and wired to the real route, permission, and navigation (`cvg010-19`). The blocked-work rendering (`cvg010-16`) needed explicit recovery choices rather than a generic error state — when future operators hit a consumption wall, the interface has to tell them what their options actually are, not just that something failed. Accessibility and failure state verification (`cvg010-20`) followed UI wiring rather than preceding it, which is the order I prefer: verify the states that will actually exist in the rendered component rather than speculating about them during construction. Backend and changed-code gates (`cvg010-21`) ran clean, documentation published (`cvg010-22`), evidence reconciled and archived (`cvg010-24`).

Beyond CVG-010, there were several boundary-level corrections across other feature areas that are worth naming because they're the kind of thing that quietly breaks consistency if left open. On the compliance side, I added two constraints: skipping owner adapters when their metadata is unavailable, and requiring a complete stored-purposes set before any digest operation proceeds. The second one is a correctness gate — a partial digest is worse than no digest because it creates a record that looks complete but isn't. The impersonation feature now enforces the aware-route gate for cookie API requests, closing a path where an impersonating session could reach the cookie API without the guard firing. Billing got a policy-hold on capability spend to bind it to the reviewed policy document rather than whatever the current runtime state happens to be. On the service side, actor identity now propagates into ticket imports, which was a missing attribution link — without it, imported tickets have no traceable origin actor. And on the privacy side, I validated exact declaration envelope identity and scope, plus inventoried legacy category consumers, both of which feed directly into the privacy-category-management work that still has open questions about version identity delegation from yesterday.

The CVG-010 closure narrows what's left in the capability governance track considerably. The next feature set in that sequence (`cvg-011` or adjacent) can now import the admission and transfer interfaces rather than speculating about what they'll look like. The unresolved question I'm carrying forward is from compliance: whether requiring a complete stored-purposes digest before any record proceeds should eventually become a database-layer constraint rather than a service-layer guard. Right now it's enforced in code, which is testable and visible, but it's also bypassable if someone goes around the service. I haven't decided yet whether the safety gain from a schema-level constraint outweighs the migration cost when the purposes model is still receiving new fields.
<!-- Generated by dev-tracker publish_to_jekyll.py (AI mode) -->
<!-- accomplished-date: 2026-09-25 -->
<!-- unit-ids: col-6038-inventory-consumers,cvg010-02,cvg010-04,cvg010-22,cvg010-24,cvg010-01,cvg010-07,cvg010-09,cvg010-16,cvg010-03,cvg010-05,cvg010-06,cvg010-08,cvg010-10,cvg010-11,cvg010-12,cvg010-15,cvg010-18,cvg010-19,cvg010-13,cvg010-14,cvg010-20,cvg010-21,privacy-validate-exact-declaration-envelope-identity,frontend-remove-conflicting-fieldset-live-value,compliance-skip-owner-adapters-with-unavailable,compliance-require-complete-stored-purposes-digest,synthetic-scenario-new-entries-completed-beat-execution,service-propagate-actor-into-ticket-imports,impersonation-enforce-aware-route-gate-cookie-api,billing-hold-capability-spend-reviewed-policy -->

<!-- accomplished-unit-ids: billing-hold-capability-spend-reviewed-policy,col-6038-inventory-consumers,compliance-require-complete-stored-purposes-digest,compliance-skip-owner-adapters-with-unavailable,cvg010-01,cvg010-02,cvg010-03,cvg010-04,cvg010-05,cvg010-06,cvg010-07,cvg010-08,cvg010-09,cvg010-10,cvg010-11,cvg010-12,cvg010-13,cvg010-14,cvg010-15,cvg010-16,cvg010-18,cvg010-19,cvg010-20,cvg010-21,cvg010-22,cvg010-24,frontend-remove-conflicting-fieldset-live-value,impersonation-enforce-aware-route-gate-cookie-api,privacy-validate-exact-declaration-envelope-identity,service-propagate-actor-into-ticket-imports,synthetic-scenario-new-entries-completed-beat-execution -->
<!-- SECTION: ACCOMPLISHED END -->
<!-- Generated by dev-tracker build_today_plan.py -->
