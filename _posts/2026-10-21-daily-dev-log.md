---
layout: post
title: "Daily Dev Log - 2026-10-21"
date: 2026-10-21
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- publication-digest: 6007cca1b9578a57631415d55aae758f2c6b279acb26fa7e9aa784a57d384fe1 -->
<!-- publication-revision: 8637cc773767470d9715d01e8c816bdc -->
<!-- plan-generated: 2026-10-21T13:30:16.096314+00:00 -->

## Today's Plan

Wednesday. Yesterday's output landed a lot of completed items but didn't follow any plan I'd written — the actual work was DSR declaration work, compliance rebuilding, bookings notice authority, and privacy catalog proofs. The `platform-state-machine-remediation-20261016` items I've named in each prior plan are still showing as in-progress rather than closed. At some point the plan and the actual work have to converge, and today I'm going to try to understand whether that's a sequencing problem or whether I'm overestimating how closeable these items actually are right now.

### Main Focus

**Produce closed artifacts for `sma-admission-owners`, `sma-admission-evidence-scope`, and `sma-admission-contracts`.** I've had these three in the plan for several consecutive days. What landed instead was DSR work and privacy category proofs — genuinely useful output, but it means these state machine admission items have been accumulating plan appearances without corresponding closed evidence. The concrete dependency path: `sma-admission-owners` records who owns and reviews what, `sma-admission-evidence-scope` records the isolated and staging scope those owners are responsible for, and `sma-admission-contracts` reviews the governed mutation risk contracts that sit on top of that. You can't review the risk contracts meaningfully without the owner assignments being explicit. And those contracts are the upstream gate for `aa-decision-reconcile` and `aa-decision-revocation`, which have been sitting in the Blocked section for long enough that I've stopped counting. Today's output is either a closed artifact from each of these three, or a written technical description of the specific obstruction — not "progressed."

**Advance `pbej-coverage-contract` and `pbej-restriction-contract` in `privacy-booking-email-journey`.** The plan has been live for 19 days. This week's work on bookings notice authority, the D15 Postmark boundary enforcement, and the comms delivery layers has created actual ground under the email journey that wasn't there last week. The coverage contract (`pbej-coverage-contract`) maps the complete owner evidence for the cohort — I need that map before `pbej-coverage-prove` can produce anything verifiable. The restriction contract (`pbej-restriction-contract`) traces the Consent unsubscribe and DROP source admission — those two are structurally upstream of the restriction proof (`pbej-restriction-prove`) and the restriction implementation (`pbej-restriction-implement`). The D15 enforcement landing yesterday makes this the right moment to close the contract layer before the distance between the infrastructure work and the contract evidence grows again.

**Close `asie-evidence-redaction-cleanup` and `asie-reviewed-receipt-closeout` as a matched pair.** The appointment-scheduling-integrated-staging-evidence plan has been open for 87 days. Both items are in Ready to Start. I've written about these in previous plans without acting on them, which suggests I've underestimated how much the redaction verification work will surface — or I've been wrong about that and it's actually just scheduled inertia. The only way to find out is to do the redaction verification and see what it reveals before trying to publish the receipt. If the redaction pass surfaces something unexpected, that becomes the named obstruction. If it doesn't, the receipt closes same session.

**Decide the concrete next step for `col-6038-scheme-successor-contract` and `col-6038-scheme-successor-storage`.** Both were progressed yesterday without closing. The scheme successor publication PR (#7873) landed yesterday, which means the successor contract and storage work are either already resolved by that merge or there's a residual gap that needs naming. I'd rather spend 20 minutes verifying which of those is true than schedule these for a seventh consecutive day. If the merge closed the functional requirement, I mark them done. If not, I write the specific delta.

### Secondary Work

**Assess `sma-integrated-acceptance-matrix` and `sma-integrated-acceptance-closure`** — these two are in Ready to Start and represent the final reconciliation layer for the state machine remediation plan. Getting the admission items closed first is the right sequence because the acceptance matrix is supposed to reconcile both gates and residual risks, and I can't produce a credible matrix without the admission evidence being settled. If the main focus admission work lands, these two become the natural continuation.

**Check whether `edp-health-contract` and `edp-health-observation` in `evidence-driven-productization` can be addressed together.** The health contract defines the observed API health contract; the observation item replaces synthetic health and latency. These two are structurally paired — the contract has to precede a meaningful observation implementation. The EDP work has had significant focus this week and I touched it a couple of days ago. These two items are concrete enough that I can produce something closeable without needing to reload the entire feature set.

### Maintenance

**Refresh the PHP test report by running `make test-fixed-batches-quick`.** The current test snapshot is 83 days old. That's long enough that the failure count — 0 passed out of 1583 — may be measuring a configuration state that no longer exists. Running the quick batch will tell me whether I have real failures to triage or a stale environment snapshot. I'm not treating 1583 failures as real until I have a current observation.

**Draft the implementation plan for `migration-safety-schema-guards`.** This is in the Planning Pipeline under "Needs Implementation Plan" — the research artifact `migration-guard-audit.md` exists. Schema migration guards are directly adjacent to the governance mutation and versioning work I've been doing in `privacy-category-management`. The audit exists; translating it into a concrete implementation plan is bounded work that unblocks future scheduling.

**Scan Markdownlint issues in the `platform-state-machine-remediation-20261016` planning directory.** There are 61 Markdownlint issues across 4 files, and I'm already touching that directory today for the admission closure work. Running `markdownlint docs/work/planning/platform-state-machine-remediation-20261016/` will surface whether any issues are in files I'm actively editing, so I can fix them in-place rather than scheduling a separate cleanup pass.

**Refresh the TODO inventory using the todo-cleanup script.** The last refresh was 90 days ago. With the volume of work that's landed since then — the privacy category management build-out, the D15 enforcement, the DSR export work — the current inventory of 0 tracked items is almost certainly wrong. A fresh run will surface any TODO markers that have accumulated in the new code, and the output is immediately usable for prioritization.

### Parked

The blocked `agent-auth-audit-remedation` items — `aa-decision-reconcile`, `aa-decision-revocation`, `aa-audit-envelope`, and `aa-test-audit-envelope` — remain parked. Their unblock path runs through the admission contracts review I'm targeting today. If `sma-admission-contracts` closes, that removes the named dependency and I can schedule these for tomorrow with a concrete basis rather than another deferred appearance.

The `browser-experience-closeout` and `public-offering-discovery-distribution` feature sets have no recent activity and aren't adjacent to today's work. I'm not scheduling them because nothing in today's plan creates useful information for those items, and loading that context would fragment rather than focus the day.

The `evidence-driven-productization` main cluster — `edp-operator-contract`, `edp-release-admission-enforcement`, `edp-operator-local-proof` — is parked in favor of the health contract pair in Secondary Work. The operator contract work requires the release evidence contract (`edp-release-evidence-contract`) to be settled first; I'd rather confirm that dependency exists before scheduling it.

<!-- plan-unit-ids: agc-00-owner-admission,col-6038-determination-model,col-6038-scheme-migration,edp-owner-reconciliation,pbej-admission,sma-admission-owners,sma-finance-gate-recovery,sma-notice-gate-gate-one -->
<!-- SECTION: DAILY-PLAN END -->


<!-- SECTION: ACCOMPLISHED START -->
<!-- publication-digest: 06cf733f925ed00b0d5c837986ed0bf7137c820178456f6a790ecc3b41beabf0 -->
<!-- publication-revision: ce05b8a102974740a841de085731511a -->
<!-- accomplished-generated: 2026-10-22T02:37:44.090814+00:00 -->

## Today's Update

Today was a convergence of security hardening, governance infrastructure, and the beginning of what I'm calling the digital sovereignty audit — three threads that are related in ways that aren't obvious until you're deep in the middle of them.

The security work came first and was the most contained. I patched the PHP image selections and enforced FPM hardening, refreshed the certifi bundle and verified the artifacts, and made Telescope capture opt-in with credential redaction. That last one is the one I'd have regretted skipping: Telescope capturing credentials by default is the kind of thing that's completely benign until it isn't, and in a multi-tenant environment where future operators will have varying levels of access to debug tooling, the safer default is no capture unless explicitly enabled. I also ran focused checks across isolated branches to validate the changes held together — not glamorous, but necessary before any of this goes further downstream. The credential header scrubbing work extended this into a separate security item: proving that capture defaults are what I think they are, not what I assume them to be.

The CI work was closely related in spirit. I established guards that refuse a production deploy unless the target environment already exists as protected, require independent review with no admin bypass on guarded environments, and reject malformed reviewer configurations. Removing the bypass flags from the protected-environment guard was the piece I felt most clearly about — bypass flags on a guard are the guard quietly lying about its own strength. What these four controls together establish is a CI posture where the pipeline can't be talked into doing something unsafe through misconfiguration alone. That's a meaningful property to have defined before any of this path is ever exercised against a real deployment.

The release authority governance work ran alongside all of this and is the most forward-looking of the day's threads. I completed the inventory of existing signing, custody, evidence, and admission mechanisms (RA-01), then made meaningful progress on the authority model (RA-02), repository controls (RA-04), and protected policy custody with verifier integrity (RA-03). These are connected: you can't define approval authority meaningfully until you know what you're approving, and you can't trust the custody chain until the repository controls that protect it are qualified. The inventory was the prerequisite; the rest are in motion. The compliance work echoed this — verifying scheme publication trigger definitions, preserving scheme catalog and policy admission tests, and scoping owner diagnostics to category schemes are all about making sure the catalog layer has a coherent contract before anything writes to it with tenant context.

The digital sovereignty audit is the thread I'm most uncertain about in terms of scope. I captured the audit mandate and current source baseline (DSA-00), mapped actor powers and institutional dependencies (DSA-01), assessed S01 through S18 by actor and failure scope (DSA-02), traced central dependencies and minimal structural options (DSA-03), designed sixteen adverse-condition exercises (DSA-04), started reconciling jurisdiction and operator obligations with counsel (DSA-05), and reviewed minimum remedies costs and owner-bound decisions (DSA-06). All of these are still in progress, which is honest — this audit is genuinely more open-ended than most of what I work on, and the legal reconciliation piece in particular doesn't have a tidy resolution yet. The adverse-condition exercises are the part I think will be most useful when this is complete: sixteen named scenarios is enough to reason about failure modes structurally rather than case by case. The state machine remediation items — owner and reviewer assignments, evidence scope recording, mutation risk contract review, and the Gate 1 receipt — were woven through all of this as bookkeeping that needed to stay current. The privacy-booking email journey work closed two evidence contracts: mapping complete owner evidence for the cohort, and tracing the consent unsubscribe and DROP source admission path. The email work restored the integration service type rollback and generated current public unsubscribe and message links — both of which matter for future tenant comms correctness. The billing account identity admission through Core Tenancy and the cohort retention through inactive authoring rounded out the day's edges.

What tomorrow looks like depends partly on where the DSA legal reconciliation lands. The RA-02, RA-03, and RA-04 items are close enough to done that they should close before anything else opens in that governance thread.

<!-- accomplished-unit-ids: aa-controller-billing-account-identity,ci-refuse-production-deploy-unless-its,ci-reject-unverified-protection-malformed-reviewers,ci-remove-bypass-flags-from-protected-environment,ci-require-independent-review-admin-bypass,compliance-preserve-scheme-catalog-policy-admission,compliance-scope-owner-diagnostics-category-schemes,compliance-verify-scheme-publication-trigger-definitions,decisions-expose-unproven-reminder-delivery-owner,decisions-read-only-reminder-claim-inventory,email-generate-current-public-unsubscribe-message,email-restore-integration-service-type-rollback,pbej-coverage-contract,pbej-restriction-contract,privacy-retain-actual-cohort-through-inactive,ra-01-authority-inventory,security-hardening-certifi,security-hardening-php,security-hardening-telescope,security-hardening-validation,security-scrub-credential-headers-prove-capture,sma-admission-contracts,sma-admission-evidence-scope,sma-admission-owners,sma-notice-gate-gate-one -->
<!-- SECTION: ACCOMPLISHED END -->
