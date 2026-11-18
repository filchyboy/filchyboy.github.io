---
layout: post
title: "Daily Dev Log - 2026-11-17"
date: 2026-11-17
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- publication-digest: be3dc76259306db0fccdf22981fe9b0ea4d5241276e2dea68c80f889e99d046f -->
<!-- publication-revision: 28ed6d3b599540e28a44988b3fa49b61 -->
<!-- plan-generated: 2026-11-17T20:30:58.026008+00:00 -->

## Today's plan

Yesterday brought progress across staging evidence, administration, provider safeguards and development tooling. I want today’s plan to show what that work makes possible and which decisions still need evidence. This is a late revision: it draws on the current captured tracker history, including the recorded distinction between the accepted private staging baseline and M1’s separate admission workflow. Those records help me separate follow-through on implemented behavior from choices that still need an owner or an observation.

### Main Focus

The first wedge remains one customer booking one fixed-location, in-person appointment, either free or fully prepaid. Confirmation, capacity, payment and later changes have to agree when that journey is interrupted. I’ll start with the confirmation and expiry work already recorded under agc-01-confirm-admission and agc-01-expiry-disposition, compare it with one candidate’s acceptance evidence, and identify the exact remaining case that needs a test or repair. An uncertain payment should keep its capacity protected; a definitively abandoned hold should release through the owner; an accepted confirmation retry should preserve the recorded result. This gives the next implementation choice a concrete basis. The accompanying agc-00-owner-admission and agc-00-contracts work needs to make the acceptance owner and unresolved authority or mutation decisions explicit. (`agc-00-owner-admission`, `agc-00-contracts`, `agc-01-confirm-admission`, `agc-01-expiry-disposition`)

I’ll use the current private staging baseline when reviewing the next deployment step. The latest history under asie-mac-mini-m1-signed-admission records that M1-only findings do not reopen that accepted private deployment gate. It also records a drafted registration source fix and a proposed reusable deployment procedure. The useful planning work is to review that fix and settle the procedure’s location, first scope, controlled repeat and treatment of read-only stages. A reusable procedure should connect pinned inputs, preflight, activation, undo, verification and a concise receipt, so a later run can show what changed and how recovery worked. The proposal itself authorizes no target execution. I’ll keep M1’s remaining admission status separate from that procedure review and from the wider appointment journey’s acceptance. (`asie-mac-mini-m1-signed-admission`)

### Secondary Work

The operator evidence remains useful follow-on work under edp-operator-local-proof and edp-operator-decision-recovery. Earlier browser receipts cover specific interruption, readback and recovery cases. I’ll reconcile those observations with the current pin and workspace behavior, then identify which cases the candidate needs before installed verification. That matters because a locally successful recovery case is evidence to build on, while owner acceptance and full installation still need their own results. I’ll keep this progress visible without asserting that all operator work is a prerequisite for the first appointment proof. (`edp-operator-local-proof`, `edp-operator-decision-recovery`)

For transactional email, agc-04-d15-email-provider-boundary already has implementation and qualification history. I’ll use that history to identify the remaining release-enforcement ownership and candidate work before proposing another provider-boundary change. The point is to close a specific remaining boundary or acceptance gap while giving credit to the implementation already recorded. A tracker’s in-progress label alone is not enough reason to repeat that work. (`agc-04-d15-email-provider-boundary`)

### Maintenance

The reporting acceptance check stays concrete under oapr-brief-context and oapr-private-transport: the consumer must use the same captured edition, the final brief must carry the right source identity, and the vault copy must pass readback with its local index intact. I’ll retain the original edition when a late recovery is needed, record the actual completion time and check retries for duplicates or overwritten edits. The result that matters for the recurring process is a natural morning run completed before 06:30 Pacific. A manual recovery or a successful transport check supplies evidence for part of that chain; it cannot establish that deadline result. (`oapr-brief-context`, `oapr-private-transport`)

### Parked

The bounded offer still follows prospect qualification and the applicable staging review under appointment-qualified-prospect-proof-01, appointment-qualified-prospect-proof-02 and appointment-qualified-prospect-proof-03. I’ll use that order when preparing the evidence for a consenting prospect cycle. The accepted private baseline does not itself establish commercial admission or a buyer outcome. Broader appointment variants and production promotion retain their separate decisions, so I won’t use this report to move them into the first bounded journey. (`appointment-qualified-prospect-proof-01`, `appointment-qualified-prospect-proof-02`, `appointment-qualified-prospect-proof-03`)

<!-- plan-unit-ids: selection-11f5a4029ce9fb5978e01f941b8647a099780572889614abf1b5fbed92fef647 -->
<!-- SECTION: DAILY-PLAN END -->


<!-- SECTION: ACCOMPLISHED START -->
<!-- publication-digest: e214ad46dbfbc63e726207b242072cef724398dcd3847987f4870bd9e78b121c -->
<!-- publication-revision: 272277d51e8247ef8dc74189a6226b5f -->
<!-- accomplished-generated: 2026-11-18T13:35:37.710416+00:00 -->

## Update for 2026-11-17

Evidence captured on 2026-11-18 for this retrospective.

### Service operations

I connected service intake to customer cases and carried the exact plan through approval, assignee acknowledgment and milestone tracking. The scoped checks give me a path to verify the whole case journey on one candidate. I still need integrated acceptance before treating these slices as a served customer workflow.

### Privacy and admin

I qualified the Suppression Management candidate locally while the installed SPA retained serving ownership. The DSR detail work also verifies that action receipts match the reviewed request and replaces stale controls after a conflict. I’ll carry both through their own installed checks before claiming wider acceptance.

### Staging preparation

I moved the private staging procedure from proposal to an implemented core, adapter, command line and bounded rehearsal. The capture and probe runbooks make the next evidence easier to interpret. Those records still leave target-specific acceptance and native admission separate from the implementation. (`asie-mac-mini-m1-signed-admission`)

### Development tooling

The real-tree comparison advanced the evidence for an advisory scan. The next decision is how to triage and retain a baseline. I’m keeping the reported findings separate from confirmed issues and leaving gate rollout open.

### Source and test maintenance

I refreshed stale privacy source registrations against the current files and repaired Billing test fixtures to set up their account context explicitly. Those changes restore the intended source checks and let the Billing tests exercise the existing guard through ordinary setup. Dependency updates also merged; I’ll keep their validation separate from product acceptance.

<!-- accomplished-unit-ids: selection-033d6330dfeae78cbeafc6321ca267842b1eaa0a589d25ab9b2707a5c009e435 -->
<!-- SECTION: ACCOMPLISHED END -->
