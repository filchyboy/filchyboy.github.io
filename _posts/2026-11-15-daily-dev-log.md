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

