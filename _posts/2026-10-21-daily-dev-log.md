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
<!-- publication-digest: baab8ea8ea1fce5be8981beb02cc873a9b58ac27870ea2507e5334cb870a435c -->
<!-- publication-revision: 61300962c1754cffa7d25e4312fcc974 -->
<!-- accomplished-generated: 2026-10-22T13:28:45.675010+00:00 -->

## Today's Update

Today was a security and governance day — not in the abstract sense, but in the concrete sense of locking down specific surfaces before they become load-bearing in future operator workflows.

The security hardening work formed the clearest thread. I patched the PHP image selections and enforced FPM hardening at the container level, refreshed the certifi bundle and verified the resulting artifacts, and made Telescope capture opt-in with credential redaction. That last one is the one I care most about: a debug tool that eagerly captures everything is fine during early development and quietly catastrophic once secrets start flowing through request headers in real workflows. The opt-in default and the scrubbing logic needed to exist before any of the tenant authentication paths get exercised under realistic conditions. The header scrubbing work ran in parallel — proving that capture defaults don't leak credential headers regardless of what Telescope's own config says. I ran focused checks and isolated branch reviews to validate all of it, which gave me confidence the hardening is actually in effect rather than just configured.

The CI pipeline controls consumed a substantial portion of the day and are worth explaining in sequence because the order mattered. First, I established that a production deploy must be refused unless the target environment already exists with protection in place — no deploying into an unprotected environment and hoping the protection gets applied after. Then I required independent review with no admin bypass on guarded environments. Then I removed the bypass flags from the protected-environment guard itself. Then I added rejection logic for unverified protection states and malformed reviewer lists. Each step tightens a specific gap that the previous step exposed: once you decide production requires a protected environment, you immediately have to ask what happens if someone with admin rights bypasses the review requirement, and once you answer that, you have to ask what a "malformed reviewer" looks like in the guard logic. The four steps aren't parallel — they're a chain where each one is the precondition for the next being meaningful.

The release-authority governance work completed RA-01 — an inventory of the existing signing, custody, evidence, and admission mechanisms — and made meaningful progress on RA-02 through RA-04. RA-02 is defining release-policy ownership and independent approval authority, RA-03 is establishing protected policy custody and verifier integrity, and RA-04 is qualifying repository review and branch-protection controls. All three are in progress rather than closed, which is honest: the inventory in RA-01 surfaced enough about the current state that the authority model needs careful definition rather than a quick pass. The digital-sovereignty audit work (DSA-00 through DSA-05) is in a similar state — baseline captured, actor powers mapped, the control matrix assessed across S01 through S18, and sixteen adverse-condition exercises designed and qualified. DSA-05, which involves reconciling jurisdiction and operator obligations, is the one I'm genuinely uncertain about in terms of scope. That's not a technical question; it's a legal and regulatory one, and the boundary between what I can resolve internally versus what requires external input isn't fully clear to me yet.

The compliance and decisions work closed out several smaller but specific contracts. Scheme publication trigger definitions got verified, scheme catalog and policy admission tests were preserved, and owner diagnostics got scoped to category schemes rather than applying across the board. On the decisions side, I exposed unproven reminder delivery in the owner readback and added a read-only reminder claim inventory — the readback change matters because a delivery that's recorded but unproven shouldn't look the same as one that's been verified, and collapsing that distinction in the owner view would make future audit work significantly harder. The privacy-booking-email-journey work traced consent unsubscribe and DROP source admission, and the email work restored integration service type rollback and generated the current public unsubscribe and message link structure. The state machine remediation thread continued with owner and reviewer assignments recorded, isolated and staging evidence scope documented, governed mutation risk contracts reviewed, and Gate 1 receipt confirmed.

The forward shape is clearer now than it was this morning. The CI controls and security hardening give me a deployment path with actual enforcement semantics rather than aspirational policy. The release-authority governance work will determine who owns what decisions in that path — and until RA-02 and RA-03 close, the authority model is defined in terms of what exists rather than what's been formally designated. That gap is the thing I'll be working against tomorrow.

<!-- accomplished-unit-ids: aa-controller-billing-account-identity,ci-refuse-production-deploy-unless-its,ci-reject-unverified-protection-malformed-reviewers,ci-remove-bypass-flags-from-protected-environment,ci-require-independent-review-admin-bypass,compliance-preserve-scheme-catalog-policy-admission,compliance-scope-owner-diagnostics-category-schemes,compliance-verify-scheme-publication-trigger-definitions,decisions-expose-unproven-reminder-delivery-owner,decisions-read-only-reminder-claim-inventory,email-generate-current-public-unsubscribe-message,email-restore-integration-service-type-rollback,pbej-coverage-contract,pbej-restriction-contract,privacy-retain-actual-cohort-through-inactive,ra-01-authority-inventory,security-hardening-certifi,security-hardening-php,security-hardening-telescope,security-hardening-validation,security-scrub-credential-headers-prove-capture,sma-admission-contracts,sma-admission-evidence-scope,sma-admission-owners,sma-notice-gate-gate-one -->
<!-- SECTION: ACCOMPLISHED END -->
