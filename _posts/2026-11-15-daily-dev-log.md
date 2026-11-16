---
layout: post
title: "Daily Dev Log - 2026-11-15"
date: 2026-11-15
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- publication-digest: affab012f8c927bc1ccd2862cb05043c4bf523ef013ed168414870ff98028d8a -->
<!-- publication-revision: de5ededc51f04742b5fa030adf33d62e -->
<!-- plan-generated: 2026-11-15T19:09:21.504035+00:00 -->

## Today’s Plan

Yesterday’s records show progress on onboarding ownership, versioned projections and the foundations for mobile work. They also leave an incomplete picture of the day. Today’s code history adds work that a tracker-only summary would miss: the operational workspace is handling interrupted reads and pin changes more carefully, and queue failure auditing now validates the tenant before attributing a failure to it. Those changes deserve to appear in the account of progress, even while their broader acceptance remains open.

For the rest of today, I want to connect that activity to a concrete product outcome: the first appointment journey that works all the way through. This is a revised plan written after work has already happened, rather than a reconstruction of what I committed to this morning.

### Main Focus

The first appointment wedge is deliberately small: one customer books one fixed-location, in-person appointment, either free or with full prepayment. But “small” still has to include the awkward parts. The customer needs a reliable confirmation and a way to change or cancel the booking; the organizer needs to cancel it correctly; capacity, payment and notifications need to agree when something goes wrong. A successful booking screen alone would leave too much of the product unfinished.

I’ll start with the existing confirmation and hold-expiry work, `agc-01-confirm-admission` and `agc-01-expiry-disposition`. Both already have implementation behind them. The useful next step is to establish what the current candidate actually proves. In particular, an uncertain payment outcome must keep the appointment’s capacity protected, ordinary abandonment must release it correctly, and a confirmation must recheck the current offering and reservation without breaking a legitimate retry. I want one evidence record connecting those cases to the same candidate, with any failure leading to a specific repair rather than another broad implementation task.

The immediate dependency is getting that candidate and its acceptance responsibilities explicit. `agc-00-owner-admission` still records outstanding named implementer and reviewer assignments, and `agc-00-contracts` remains open. I’ll reconcile those records with the owners’ current work, identify who can accept each part of this bounded journey, and make the outstanding decisions concrete. The old portfolio exception proposal has expired; it needs a current disposition rather than being carried forward as assumed permission. That unrelated portfolio issue should retain its own record, while the appointment work gets a clear execution boundary.

### Secondary Work

The operational workspace is another place where finishing the behavior matters more than moving another item into progress. Today’s changes address a subtle interruption case: a pin write can commit after a newer workspace read has already displayed the old state. The follow-up requests a fresh authoritative read without replaying the write, and prevents an old completion from taking over a replacement session.

I’ll carry that through the operator journey under `edp-operator-local-proof`, alongside `edp-operator-decision-recovery`: make a choice, interrupt the session, recover, and check that the visible result agrees with the durable state. The existing browser evidence and today’s follow-up belong to different revisions, so I need to bring the relevant checks together before treating the whole recovery path as qualified. This work is useful beyond appointments, but I won’t turn it into an appointment dependency without evidence that the journey needs it.

For transactional email, `agc-04-d15-email-provider-boundary` already has Postmark-only enforcement and recorded qualification against an earlier integration candidate. I’ll use that work as the starting point, check what has changed since its qualification, and resolve the remaining release-enforcement ownership before selecting the necessary reruns. Reimplementing the boundary would add work without closing the actual gap.

### Maintenance

The reporting repair needs to finish as an operating process. Under `oapr-brief-context` and `oapr-private-transport`, I’ll connect the richer private context to the actual reporting execution, check that the public account draws from current sources, and settle which producer owns each dated post. The repaired process needs to preserve edits, avoid duplicate publications, and distinguish yesterday’s accomplishments from today’s plan and tonight’s update.

The deadline is completion before 06:30 Pacific, including delivery, not starting a job at 06:30. Local rehearsals help qualify the components; the remaining proof is an unattended run that delivers substantive reports on time.

I’ll also keep today’s queue failure-audit change visible in the work record. Its source change validates the account before attributing a failed job to that tenant. That is concrete work outside the appointment checklist, and it should be reported with its own evidence rather than assigned an unrelated tracker ID.

### Parked

I’m keeping broader appointment variants and production promotion outside this first journey. They need their own evidence and decisions; adding them now would make it harder to see whether the bounded appointment experience is actually complete.

Further native mobile implementation remains separate from its completed foundation work. Additional data imports also remain outside the currently authorized work. Neither needs to disappear from the longer-term plan, but neither should displace the current appointment acceptance work or be described as already delivered.

<!-- plan-unit-ids: human-reviewed-7d619ed213fa28cc47fb23ff478aa86de2097fc28359f1dc020af0190bcb6de0 -->
<!-- SECTION: DAILY-PLAN END -->


<!-- SECTION: ACCOMPLISHED START -->
<!-- publication-digest: 7abdb5a78bb8ee71b6ac59828068cba8f6bc00508959cb97d957b023421221d7 -->
<!-- publication-revision: e4d81b8a164548a8a75db5f707566135 -->
<!-- accomplished-generated: 2026-11-16T16:11:13.356465+00:00 -->

## November 15 Update

*Partial retrospective, prepared November 16.*

The clearest reporting progress was connecting the evidence to a useful account of the work. I published the revised daily plan after review, restoring meaningful priorities, concrete appointment work and searchable tracker IDs. I also restored the November 14 update as a qualified partial recovery. That repaired the public account without pretending that the missing history had been captured at the time.

### Reporting and Delivery

Under `oapr-brief-context` and `oapr-private-transport`, I connected a bounded export of project context and a matching source assessment to the private input Page. Actual file readback and the consumer checks matched the captured edition and source revision. The input could now carry goals, blockers, ownership and next actions rather than counts alone.

The review also caught substantive problems in early candidates: weaker offer prerequisites, missing staging limitations, omissions of current work, and a claim that suggested more runtime acceptance than the record established. Correcting those findings improved the account before any further publication.

The delivery rehearsals crossed review, exact-grant issuance, local writing, Git delivery and rendered readback in isolated fixtures. Repeating them produced no duplicate post or commit, and the update preserved the existing morning plan. The focused run reached 152 passing tests. Those checks qualify the tested paths; they do not establish that the scheduled morning process completed on time.

I installed the approved routine reporting policy and a quiesced cutover control. The new public worker remained paused, and the control blocked publication while the remaining integration was open. Existing grants and published posts were preserved. Recording the real worker execution and completing the coordinated cutover remained unfinished.

### Staging Progress

The work under `asie-mac-mini-m1-signed-admission` made the next staging choice more concrete. A read-only connectivity check timed out on the proposed publication route. The subsequent review compared the available paths and recorded the choice of a reviewed client inside the existing application environment. That narrowed the next piece of work without changing the existing guard or claiming M1 admission. The task remained deferred.

### What Carries Forward

The appointment confirmation and hold-expiry work, `agc-01-confirm-admission` and `agc-01-expiry-disposition`, already had implementation in the record. I did not establish a new completed customer journey on November 15. The useful follow-through is to bind the relevant cases to a current candidate and its acceptance owners, while keeping the separate staging and operator checks within their own scopes.

The remaining reporting proof is operational: one owner for each stage, the matching context reaching the actual brief producer, complete delivery and archive receipts, and a natural run finishing before 06:30 Pacific. The isolated archive qualification verified the original brief and duplicate-safe retries; it did not qualify the recurring import or an on-time run.

<!-- accomplished-unit-ids: human-reviewed-12dae2cfc685f1c7fc033122327526ff052497958db3296e6f4963ac99af83bc -->
<!-- SECTION: ACCOMPLISHED END -->
