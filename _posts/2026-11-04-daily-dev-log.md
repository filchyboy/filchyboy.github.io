---
layout: post
title: "Daily Dev Log - 2026-11-04"
date: 2026-11-04
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- publication-digest: 4e6034ff49efb3a849475d89ae7c05edfe29e9546f2d654524b42da3b98200cf -->
<!-- publication-revision: 2a9b88bd725c438cbe38e7428bc8c95f -->
<!-- plan-generated: 2026-11-04T14:08:40.336682+00:00 -->

## Today's Plan

Wednesday. Yesterday I did four admin journey repair items, an audit record, a security digest entry, and the tv713 planning documentation — none of which appeared in any plan I'd written. That's fine. The admin shell work was real and needed doing. What it means for today is that I'm not pretending `asie-mac-mini-private-functional-completion` is going to be the focus if something else keeps finding its way to the top of the queue. It's appeared in every plan for two weeks. I'm going to describe what actually needs to happen there, and if I do it today, great.

The more interesting thing to name this morning: the MFA page health chain finished closing yesterday — fourteen PRs merged across state shape diagnostics, health log deployment, checkpoint detail windows, and native results. That's a dense run. The external-agent-surface-preconditions set also got touched in the last 24 hours, which is a different thread entirely — the principal model and consent parity work there hasn't had sustained attention, but it's live.

### Main Focus

**Advance `asie-mac-mini-private-functional-completion` through to a written deployment evidence record.** The plan's current complete window is `artifacts/dagger-disposable-lab-admission/mac-mini-private-readiness-snapshot.md`. Paths passed, startup passed, readiness held, full cleanup passed, security deferral is documented. The remaining work is reading that snapshot and producing the deployment evidence record from it. I've written this paragraph in some form for ten consecutive days. The obstruction isn't technical — it's that producing the record requires sitting with a chain of merged evidence artifacts and writing a bounded summary that doesn't overstate what the deferral covers. That's the trade-off I keep bumping against: writing a truthful receipt where the security deferral is prominent without making the receipt itself look like a failure report. I'll make that call today and write the thing.

**Move `idr-20260728-characterization` forward on the imperative-to-declarative refactor set.** This has been the heaviest-focus feature set all week beyond the venue work, and characterizing the selected refactor behavior is the foundational step before any of the actual transformation work starts. The plan shows 0 of 14 items complete with implementation not started — but the highest-leverage candidates are identified (`IDR-2026-07-28-041`, `IDR-2026-07-28-045`, `IDR-2026-07-28-043`). Characterization means writing behavioral tests or observation records against those three before touching the refactor itself. The reason to do this before anything else in that feature set: changing imperative code to declarative without first characterizing existing behavior is how you produce a refactor that "works" but subtly changes scheduling semantics.

**Work the `venue-space-holds` physical identity layer — specifically `venue-physical-schema` and `venue-physical-model`.** This feature set has had heavy focus all week and has 17 items still open. The schema migration and model are foundational — `venue-calendar-binding-schema`, `venue-calendar-binding-action`, and the query exposure all depend on the physical identity being persistent first. The sequencing argument for doing schema before model before anything else is obvious, but I want to be clear about one thing I'm uncertain about: whether the `venue-physical-owner-foundation` evidence recording needs to precede the migration or whether those can proceed in parallel. I'll check the plan's dependency notes before writing the migration.

**Close `platform-state-machine-remediation-20261016` by working through the remaining six items.** This set is 🏁 marked — the six remaining items are all review and acceptance tasks: support gate recovery, integrated acceptance matrix, acceptance closure, Gate 1 receipt, support owner staging receipt, and Commerce settlement staging receipt. These aren't implementation tasks; they're structured review steps. Six review items sitting at near-completion is a plan that closes this week, and clearing it cleans the deck meaningfully. The dependency worth checking: whether `sma-integrated-acceptance-matrix` can close before the two staging receipts are accepted, or whether the matrix depends on both owners confirming.

### Secondary Work

**Start `esp-principal-model` from the `external-agent-surface-preconditions` set.** This was touched in the last 24 hours and the work is already in motion — the external agent principal model and verification guard is the foundational item that the consent parity, delegation binding, and async context items all depend on. I want to get a concrete artifact on disk rather than leaving it as an open schema question. The principal model's shape determines whether the delegation binding in `esp-delegation-binding` is a foreign key concern or something that needs its own verification table, and I'd rather resolve that before writing the downstream items.

**Advance `sobr-journeys-remaining-1` for the remaining admin MFE wave 1 routes.** This feature set has been active all week and the journey addition work is straightforward enumeration — identifying which admin routes still lack coverage in `python3 scripts/check_surface_ownership.py` and adding them systematically. The baseline is currently 330 of 404 route files dispositioned.

### Maintenance

**Regenerate PHP test results with `make test-fixed-batches-quick`.** The last test run is 97 days old — that report is too stale to trust as a health signal. The 1583 failures in the snapshot could be environment-related regressions from infrastructure changes over that period, or they could be real. I won't know until I run it.

**Regenerate TODO inventory.** The TODO tracking is 105 days old, run with the todo-cleanup script. With the codebase at 53,061 files, an empty inventory from a stale run is meaningless data.

**Draft the `migration-safety-schema-guards` implementation plan.** This is in the planning pipeline as aligned with active work — the venue physical schema migration I'm writing today is exactly the kind of work that migration guard audit artifacts are meant to cover. The `migration-guard-audit.md` artifact exists but needs an implementation plan. While the schema migration is fresh in my head is the right moment to write this, not after I've context-switched away from the migration layer.

**Fix Markdownlint issues across the 4 affected files.** There are 61 issues tracked across 4 files. These are specific, bounded, and don't require broad auto-fix — I can open each file directly and correct them. Worth doing while I'm producing new markdown artifacts today anyway.

### Parked

`rd100v2-state-effects-warnings-wave` and `rd100v2-a11y-tail-wave` from the React Doctor followup sprint are explicitly not today's work. The 321 State & Effects warnings and ~696 accessibility warnings represent a focused remediation sprint that needs uninterrupted attention across a full block — running it in parallel with schema migrations and staging evidence work produces sloppy fixes. The `browser-experience-closeout` set (66 items, no recent activity) is similarly parked: none of those items are blocking current work and the set hasn't been touched recently enough to have an obvious entry point today. `agent-auth-audit-remedation` remains blocked — the four blocked items (`aa-decision-reconcile`, `aa-decision-revocation`, `aa-audit-envelope`, `aa-test-audit-envelope`) are waiting on dependency resolution that isn't in my control today.

<!-- plan-unit-ids: admission-ga-checkout-caller,asie-mac-mini-private-functional-completion,esp-principal-model,idr-20260728-characterization -->
<!-- SECTION: DAILY-PLAN END -->


<!-- SECTION: ACCOMPLISHED START -->
<!-- publication-digest: 8b0f027124f99b1db32b8e8310b183361d9db2b4faf05d830b52ce09e2b0709e -->
<!-- publication-revision: 58712aa4f324441e8103fd6988efe7ce -->
<!-- accomplished-generated: 2026-11-05T14:16:14.681081+00:00 -->

## Today's Update

The main story today was delivering TV716 — the agent artifact temporal neighborhood loop — from first principles through to shipped frontend integration. Eight units in sequence, all in a single feature set, which is a lot to hold together. The sequence runs: contract scope baseline, backend orchestration, data determinism, API contract hardening, observability instrumentation, quality gates and handoff, frontend integration, and focused tests with accessibility. Each stage produces something the next stage depends on, so the order isn't arbitrary. The contract scope baseline is the one I treat as the real design moment — it's where I commit to what the temporal neighborhood query is allowed to return, what the agent artifact layer is allowed to assume, and where the boundary sits between "data the backend owns" and "shape the frontend receives." Once that's locked, the backend orchestration and data determinism work become constrained problems rather than open-ended ones.

The data determinism unit is where the interesting engineering actually lives in a slice like this. Temporal neighborhood queries have a specific problem: "neighborhood" implies ordering by time, but time fields in artifact records can be duplicated or imprecise. I had to decide how ties are resolved — what the tiebreaker is when two artifacts share a timestamp — and encode that decision explicitly in the test fixtures rather than leaving it as an emergent property of whatever the database returns. That choice matters downstream. If the ordering isn't deterministic under test conditions, the API contract hardening tests can pass on one run and fail on another depending on query plan behavior, which is exactly the class of flakiness that's impossible to debug in CI without understanding the root cause. The rule I settled on is deterministic secondary sort by artifact ID, which is arbitrary but stable. I'm not convinced it's the right semantic choice long-term — artifact ID ordering doesn't necessarily reflect any meaningful chronology — but it's the defensible choice for now, and changing it later is a localized edit.

Outside TV716, three email-related items closed out the day, and they're more interconnected than the titles suggest. The retained owner attestation consumer adds the event handler that processes ownership attestation events off the queue — without it, the attestation events fire and disappear. Redacting the retained receiver key from the audit log is a data hygiene decision: the receiver key is sensitive enough that it shouldn't appear in audit trails where it might be exported or inspected by operators who have audit access but not key-management access. Closing the retained owner CLI and rollback boundaries is the piece I'd been deferring — the CLI command that manages retained ownership needed explicit rollback semantics so that a failed mid-operation state doesn't leave ownership records in a half-claimed condition. These three items form a natural completion cluster for the retained owner pathway; individually they're fine, but together they close the loop on the data flow. There was also an ADR numbering collision that needed resolving — ADR-0427 had been assigned twice, which would have created reference ambiguity in any future document that cited it by number.

One item I want to note separately: the "restore temporal comparison after context switch" unit. This was recovery work, not new work. At some point during the day's sequencing, a context switch between the email work and the TV716 work left a comparison assertion in the temporal tests in a degraded state — the assertion existed but wasn't testing what it claimed to test. Finding that mid-session is the kind of thing that's easy to miss if the test suite is still green overall, which it was. The lesson I keep relearning is that green tests aren't a sufficient signal when the underlying assertion has been silently weakened. I caught it because I was reviewing the test output carefully before closing the quality gates unit, not because CI flagged it.

The TV716 completion opens the agent artifact surface for the UI work that sits behind it. The temporal neighborhood data shape is now fully specified at the API boundary, which means the React components can be built against a stable contract rather than a moving target.

<!-- accomplished-unit-ids: adr-resolve-adr-0427-numbering-collision,email-close-retained-owner-cli-rollback,email-redact-retained-receiver-key-from,email-retained-owner-attestation-consumer,tv716-api-contract-hardening,tv716-backend-orchestration,tv716-contract-scope-baseline,tv716-data-determinism,tv716-focused-tests-a11y,tv716-frontend-integration,tv716-observability-instrumentation,tv716-quality-gates-handoff,tv716-restore-temporal-comparison-after-context -->
<!-- SECTION: ACCOMPLISHED END -->
