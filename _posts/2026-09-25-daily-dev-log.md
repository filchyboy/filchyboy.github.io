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
<!-- accomplished-generated: 2026-09-26T13:06:58.220025+00:00 -->
<!-- accomplished-updated: 2026-09-26T13:06:58.220025+00:00 -->

## Today's Update

Today was a specification closure day — three capability feature sets taken from baseline refresh through full archive, and a wide range of supporting work across analytics, billing, compliance, and infrastructure. The volume is high, but the structure underneath it is deliberate.

The three feature sets — capability consumption controls (cvg-010), platform self-governance (cvg-011), and verified transfer benefits (cvg-012) — each went through the same end-to-end sequence: refresh the scope and overlap, admit the owner interface and mutation contract, do the implementation work, test it, wire routing and navigation, and then reconcile the evidence before archiving. That's roughly twenty-two items per set, and running all three in parallel rather than sequentially was a conscious choice. The interface definitions share enough structural similarity that drafting them back-to-back surfaces inconsistencies that isolated drafting would miss — for instance, the mutation contracts for cvg-010 and cvg-011 both needed to express what happens when an admission request arrives during a quiescent state, and I'd rather those two contracts make the same guarantee than arrive at independent answers.

Within cvg-010, the most load-bearing pieces were the serialization and replay logic. Serializing ordinary budget admission and transfer window reservation separately matters because they have different idempotency guarantees — a transfer window reservation can be retried within the window, but ordinary budget admission that replays against a changed state is dangerous. I bound admission replay to an immutable request specifically to prevent that class of bug from appearing later. The competing admissions test on MySQL (`cvg010-13`) was a prerequisite for feeling confident about that boundary; I wanted proof that the lock behavior holds under concurrent access before treating the contract as settled. The `SpendControlCenter` extension with transfer scope closes out the UI side, giving future operators a single surface to see both ordinary and transfer-scoped capability consumption in context.

Platform self-governance (cvg-011) required being precise about something that's easy to elide: the difference between what the platform owns versus what a tenant owns when both are consuming the same underlying capability infrastructure. The `Define platform versus tenant scope` work isn't abstract — it determines which approval paths are available to whom, and whether a separation-of-duties policy even applies to a given action. I also added periodic review cases and the enforcement logic for independent approval where the policy requires it. The self-approval test (`cvg011-13`) is the honest test here: it's the case where a governance system most commonly fails in practice, and I'd rather have explicit proof it rejects self-approval than assume the policy propagates correctly through the agent action binding.

The verified transfer benefits set (cvg-012) has the most arithmetic surface. Computing the signed net transfer benefit, separating annualized from avoided scenarios, and preventing duplicate initiative attribution are all places where small modeling errors compound quietly. The decision to record signed transfer benefits without clamping losses in the analytics layer (`analytics-record-signed-transfer-benefit-without-clamping-losses`) was deliberate: clamping losses at zero produces a systematically optimistic picture of transfer outcomes, which is the wrong default for a system that future operators will use to make financial decisions. Whether the drilldown evidence surface is granular enough to make that loss signal actionable is something I'm less certain about — the scoped evidence drilldown exists now, but it may need additional filtering before it's genuinely useful under real initiative data.

Beyond the three capability sets, I closed a handful of things that don't fit a single theme but were overdue: propagating actor identity into ticket imports, enforcing the aware-route gate for cookie API requests in the impersonation path, requiring complete stored purposes before computing a compliance digest, and adding the GMP extension to the CI PHP setup. That last one is small but concrete — the `php-ci.yml` extension list now includes `gmp` under `setup-php`, which prevents a class of silent failures on builds that hit GMP-dependent code paths. The privacy declaration envelope validation and the frontend fieldset live value conflict are similarly contained but correct a real boundary that would otherwise produce ambiguous state when both are exercised together.
<!-- Generated by dev-tracker publish_to_jekyll.py (AI mode) -->
<!-- accomplished-date: 2026-09-25 -->
<!-- unit-ids: col-6038-inventory-consumers,test-image-gmp-extension-php-ci-alignment,cvg010-02,cvg010-04,cvg010-22,cvg010-24,cvg011-02,cvg011-03,cvg011-21,cvg011-23,cvg012-02,cvg012-04,cvg012-23,cvg012-25,cvg010-01,cvg011-01,cvg012-01,cvg010-07,cvg010-09,cvg010-16,cvg010-03,cvg010-05,cvg010-06,cvg010-08,cvg010-10,cvg010-11,cvg010-12,cvg010-15,cvg010-18,cvg010-19,cvg011-04,cvg011-05,cvg011-06,cvg011-07,cvg011-08,cvg011-09,cvg011-10,cvg011-11,cvg011-14,cvg011-15,cvg011-17,cvg011-18,cvg012-03,cvg012-05,cvg012-06,cvg012-07,cvg012-08,cvg012-09,cvg012-10,cvg012-11,cvg012-12,cvg012-16,cvg012-17,cvg012-19,cvg012-20,cvg011-13,cvg010-13,cvg010-14,cvg010-20,cvg010-21,cvg011-12,cvg011-16,cvg011-19,cvg011-20,cvg012-13,cvg012-14,cvg012-15,cvg012-18,cvg012-21,cvg012-22,privacy-validate-exact-declaration-envelope-identity,frontend-remove-conflicting-fieldset-live-value,compliance-skip-owner-adapters-with-unavailable,compliance-require-complete-stored-purposes-digest,synthetic-scenario-new-entries-completed-beat-execution,service-propagate-actor-into-ticket-imports,impersonation-enforce-aware-route-gate-cookie-api,billing-hold-capability-spend-reviewed-policy,planning-archive-platform-self-governance-evidence,planning-register-platform-self-governance-canary-follow-up,stewardship-govern-platform-services-under-same,stewardship-keep-pending-platform-review-delivery,completed-plans-completed-plans-various-features-bug,scenario-hide-studio-navigation-from-tenant,php-ci-gmp-setup-php-extensions-ops-0006,analytics-record-signed-transfer-benefit-without,analytics-archive-verified-transfer-benefit-plan,analytics-keep-transfer-benefit-verification-scoped -->

<!-- accomplished-unit-ids: analytics-archive-verified-transfer-benefit-plan,analytics-keep-transfer-benefit-verification-scoped,analytics-record-signed-transfer-benefit-without,billing-hold-capability-spend-reviewed-policy,col-6038-inventory-consumers,completed-plans-completed-plans-various-features-bug,compliance-require-complete-stored-purposes-digest,compliance-skip-owner-adapters-with-unavailable,cvg010-01,cvg010-02,cvg010-03,cvg010-04,cvg010-05,cvg010-06,cvg010-07,cvg010-08,cvg010-09,cvg010-10,cvg010-11,cvg010-12,cvg010-13,cvg010-14,cvg010-15,cvg010-16,cvg010-18,cvg010-19,cvg010-20,cvg010-21,cvg010-22,cvg010-24,cvg011-01,cvg011-02,cvg011-03,cvg011-04,cvg011-05,cvg011-06,cvg011-07,cvg011-08,cvg011-09,cvg011-10,cvg011-11,cvg011-12,cvg011-13,cvg011-14,cvg011-15,cvg011-16,cvg011-17,cvg011-18,cvg011-19,cvg011-20,cvg011-21,cvg011-23,cvg012-01,cvg012-02,cvg012-03,cvg012-04,cvg012-05,cvg012-06,cvg012-07,cvg012-08,cvg012-09,cvg012-10,cvg012-11,cvg012-12,cvg012-13,cvg012-14,cvg012-15,cvg012-16,cvg012-17,cvg012-18,cvg012-19,cvg012-20,cvg012-21,cvg012-22,cvg012-23,cvg012-25,frontend-remove-conflicting-fieldset-live-value,impersonation-enforce-aware-route-gate-cookie-api,php-ci-gmp-setup-php-extensions-ops-0006,planning-archive-platform-self-governance-evidence,planning-register-platform-self-governance-canary-follow-up,privacy-validate-exact-declaration-envelope-identity,scenario-hide-studio-navigation-from-tenant,service-propagate-actor-into-ticket-imports,stewardship-govern-platform-services-under-same,stewardship-keep-pending-platform-review-delivery,synthetic-scenario-new-entries-completed-beat-execution,test-image-gmp-extension-php-ci-alignment -->
<!-- SECTION: ACCOMPLISHED END -->
<!-- Generated by dev-tracker build_today_plan.py -->
