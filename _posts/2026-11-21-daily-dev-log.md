---
layout: post
title: "Daily Dev Log - 2026-11-21"
date: 2026-11-21
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- publication-digest: e3d333f106552a5bf72d9435e6759067ae2021a5e420e00295f25a30e26d1bb6 -->
<!-- publication-revision: 043d8e78a2e34ebc8e2b1066f22ba630 -->
<!-- plan-generated: 2026-11-21T13:41:45.593497+00:00 -->

## Today's plan

Yesterday’s work gives me concrete operator paths to qualify: venue proposals now reach a Scheduling workspace, event registration retains attendee details, and Marketing follow-through binds its original source. The remote candidate build and app-plus-renderer implementation also advance the release preparation described in yesterday’s plan. Today I’ll turn that progress into a small set of owner decisions and exact-candidate checks, while keeping the first sellable appointment journey’s acceptance separate from the surrounding platform work.

### Main Focus

I’ll start by asking the Bookings and Identity owners to reconcile the still-open appointment contracts and name one candidate for the remaining acceptance checks. Confirmation and hold expiry already have implementation; the useful next proof is that uncertain payment preserves capacity, definite abandonment releases it once and replay returns the original committed confirmation. I’ll use the current owner and contract records to identify which check can proceed, rather than treating nearby event functionality as evidence that this separate customer journey is accepted. (`agc-00-owner-admission`, `agc-00-contracts`, `agc-01-confirm-admission`, `agc-01-expiry-disposition`)

For the venue work, I’ll reconcile the new organizer workspace with the exact local deposit, confirmation and recovery evidence, then identify the deployed-candidate gap with the Events owner. The immediate question is which build and remaining story gates are needed for an observed deployed journey. I’ll preserve the successful native and browser checks at their tested scope. Venue readiness, event credentials and the appointment wedge each keep their own acceptance decision.

### Secondary Work

The release follow-through is to review the supervised native admission design with its owner, resolve the remaining choices and agree the implementation boundary. Candidate building has succeeded, and application and renderer replacement is implemented; those facts make a precise design review worthwhile. They do not lift the current hold. I’ll keep the proposed first candidate, required evidence and recovery expectations explicit before another execution window is considered.

I’ll check that form enrollment and lead qualification carry their original source identity through the documented recovery handoffs, and record the next deployment qualification boundary with their owners. For contact preferences, I’ll retain the unfinished checkpoint and identify the next admitted step before work resumes. Verified contact custody, a reviewed lead and permission to send are separate facts. Keeping those facts distinct prevents a recovered handoff from silently changing the decision it represents.

### Maintenance

I’ll read back the morning public pages and match private consumption to the canonical laptop receipt and assessment before recording delivery. For tooling, I’ll carry forward the measured real-tree scan comparison and the limited pack-window result, leaving finding review and full-run memory qualification with their owners. The corrected backend profiles still report incomplete coverage, so their successful execution will remain a diagnostic result rather than an enforcement success. (`oapr-brief-context`, `oapr-private-transport`)

### Parked

I’ll keep the bounded offer behind prospect qualification and staging review: identify a consenting prospect and the workflow question, review the applicable provider and recovery limits, then define the offer. New screens and a successful candidate build make those conversations more concrete, but neither is an observed buyer outcome. Broad M1 admission remains deferred, and the changed-image hold remains in effect until its separate approved path qualifies. (`appointment-qualified-prospect-proof-01`, `appointment-qualified-prospect-proof-02`, `appointment-qualified-prospect-proof-03`)

<!-- plan-unit-ids: selection-fb76e2cbfff09cc11f4830b413cadca24785f2cf18cfd76974ce7ed694b70352 -->
<!-- SECTION: DAILY-PLAN END -->


<!-- SECTION: ACCOMPLISHED START -->
<!-- publication-digest: a707857f5da24ba1be7ec674f9611e70786555086e7fcd0c7e917ff937304503 -->
<!-- publication-revision: 86410d24b9e548dbaa949f6afc8a14c3 -->
<!-- accomplished-generated: 2026-11-22T13:41:12.567278+00:00 -->

## Update for 2026-11-21

Evidence captured on 2026-11-22 for this retrospective.

### Period and scope

November 21 changed the appointment acceptance picture. I recorded owner-admission completion, bounded local acceptance for confirmation and expiry, and a registered-customer forfeiture path with its own explicit acceptance. The remaining contract gate is still open. This retrospective covers the completed Pacific day across the product and development-orchestrator repositories; its other major results concern agent development acceptance, Support receipt recovery and supervised release preparation.

### Appointment owner and contract decisions

The accepted owner scope now covers the preserved appointment tasks and their source boundaries, and owner-admission is marked done. That resolves the first owner-reconciliation action in yesterday’s plan. Confirmation and hold expiry also have accepted local evidence, including refusal behavior that preserves committed state. Those implementation units remain in progress because their contract and broader acceptance requirements have not all closed. (`agc-00-owner-admission`, `agc-01-confirm-admission`, `agc-01-expiry-disposition`)

The lifecycle review also accepted bounded free in-person contracts and the cutoff lifetime and evidence-allocation decisions. The source now revalidates current authority after workflow lock waits. This is a more precise basis for the next contract review: the open question is which remaining paid, delegated and source-evidence cases qualify, rather than whether any ownership decision has been made. Christopher remains the acceptance decision maker; Bookings, Identity and Commerce supply their respective evidence. (`agc-00-contracts`)

### Human approval of cancellation consequences

I implemented the first registered-customer path for cancelling an admitted fully prepaid appointment with forfeiture after the refund cutoff. The customer sees the exact current consequence and makes a separate explicit decision using the existing fresh-MFA session. Approval, required evidence, native cancellation and one-use consumption commit together or roll back together. Loading a review page or possessing an earlier lifecycle link does not make that financial choice for the customer.

Christopher separately accepted that bounded implementation and its retained local evidence. Later tests add proof at appointment-start equality, independent review expiry and a prepared second-account review. Those new cases qualify their pinned source and retain a documented expiry-fixture limitation; they are not another acceptance decision. Guest and delegated finalization, settlement and full contract conformance remain outside the accepted result.

### Agent development acceptance

The external-agent work completed bounded development acceptance for principal delegation and authorization-aware discovery. The caller evidence connects current human and source authority to the admitted operation, and confirms that a retained catalog cannot replace current execution checks. Retirement now treats required persistence as part of the result, and delegation updates preserve their intended typed resource values. These changes and tests give the original units more credible acceptance evidence without expanding the selected operation into a general release.

The underlying qualification work includes issuance, effect-fence and queued-read refusal cases. Some cohorts exercise real native workers; others are local caller observations that explicitly do not prove physical database contention. The cohorts overlap, so their totals remain attached to the original runs. Async context, consent parity and launch still retain their separate gates, and the internal provider pilot still needs its own live qualification.

### Support receipt recovery

Support qualification now checks current view authority and the original actor when recovering historical results. Further native cases recover the durable original response despite optional cache loss, preserve completed lifecycle state when receipt markers are unusable, and serialize recovery with marker deletion. That is useful evidence that a retry cannot quietly become a different operation. The broader regression timeout and the remaining missing-marker reconciliation disposition stay visible; these focused cohorts do not close the whole state-machine program.

### Supervised release preparation

The supervised native admission design is now implemented, and an exact candidate received its first reviewed admission. The early release attempts exposed transport, stack-discovery and snapshot-comparison mismatches. The later fifth attempt reached activation but refused a runtime mismatch before replacing any container, ending with no change. This advances yesterday’s design-review proposal into observed execution of the guarded path, while still falling short of a successful changed-image deployment.

The correction builds the candidate web server from the running web server’s recipe and checks runtime compatibility earlier. The rebuilt candidate passed its ARM64 build and served checks, then received a fresh admission for attempt six. That is the latest retained checkpoint: a prepared and admitted next attempt, with no successful release result in the inspected record. I’ll require that result and its verification evidence before describing the release mechanics as qualified.

### Source-owned scan controls

The owner assigned the accepted-findings baseline to the source repository. The orchestrator gained a review worksheet and explicit controls for generating that baseline, along with an owner-run positive check. The recorded positive result detects the synthetic control at its nine tested text-file locations. It does not establish coverage of every application file, every credential shape or every ignored observation, so a quiet scan remains a bounded measurement rather than a general safety claim.

The tooling follow-through also fixes path quoting in the earlier Mac scripts and adds an opt-in dependency-install profile for the PHP and Node gates. Dependencies come from the pinned manifests and locks without replacing verified source entries. Its isolated tests pass at their recorded scope; qualification of the full real-source gate run remains separate from installing the profile.

<!-- accomplished-unit-ids: selection-c94af188fd884352c1ed71071d163c7d54805e3006001de4237ba0f0c8ffa982 -->
<!-- SECTION: ACCOMPLISHED END -->
