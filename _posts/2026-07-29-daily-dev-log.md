---
layout: post
title: "Daily Dev Log - 2026-07-29"
date: 2026-07-29
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-07-30T03:28:49.413255+00:00 -->

## Today's Plan

Wednesday. Yesterday I shipped an enormous volume of codebase quality work — controller migrations, Porto gate wiring, billing tenant scope audits, the FinOps task extraction pilot — plus a full wave of horizontal slices that are now archived. The board looks genuinely different this morning. The PHPStan and documentation remediation work I've been circling back to all week is still standing, and I want to make real progress on both today.

### Main Focus

**Execute `idr-20260728-etl-descriptor-spike` — defining the local ETL descriptor shape.** I touched this yesterday and the spike is the only unit in this feature set. The declarative refactors plan (`imperative-to-declarative-refactors-2026-07-28`) sits at 0/14 units with 10 candidates planned — the ETL descriptor spike is the conceptual prerequisite for the whole set. Until I have a concrete descriptor shape, the other 13 units are working against an abstract target. The plan's three highest-leverage units (`IDR-2026-07-28-041`, `IDR-2026-07-28-045`, `IDR-2026-07-28-043`) all depend on the descriptor contract landing first. The tricky part of this spike is the boundary question: the descriptor needs to represent ETL job intent in a form that's portable across adapters, but I don't yet have a position on whether that means a data-bag struct or something with a behavioral interface. That's the spike question.

**Advance `phpstan-ratchet-knowledge-cutoff-implement` — passing effective time, knowledge cutoff, and jurisdictions correctly.** This unit has been in the ready queue all week and I keep landing adjacent PHPStan work without closing this one. The PHPStan remediation plan is at 1/22 units with a baseline of 35 findings across ten root causes. The `knowledge-cutoff-implement` unit is specifically about making sure the outbound-admission calls receive the right temporal and jurisdictional context — passing stale or zero values there creates semantic errors that PHPStan level 9 won't catch but the runtime admission contract will eventually reject. This is a correctness issue, not a style issue, which is why it's worth dedicated attention rather than bundling it with the next batch.

**Work through `dha-054-email-cdp-cutover-metadata-lint` and `dha-052-auth-waiver-frontmatter`.** The documentation hierarchy audit remediation plan has been active this week and I touched it yesterday. Both units are concrete and bounded: `dha-054` fixes email contacts CDP cutover metadata and markdownlint across whatever files that cutover touches, and `dha-052` converts auth security waiver metadata to frontmatter. The markdownlint report currently shows 2 issues across 1 file — if `dha-054` is in that file or adjacent to it, I should be able to close the linter finding as a side effect rather than as a separate pass. The auth waiver frontmatter conversion in `dha-052` is the kind of structural change that's worth doing before any documentation tooling runs another audit cycle, or the next audit will flag it again. I want both units done before the week closes.

**Sequence into the appointment scheduling staging evidence work.** The `appointment-scheduling-integrated-staging-evidence` plan started three days ago and I haven't been in it recently — the four ready units (`asie-evidence-redaction-cleanup`, `asie-bootstrap-residual-dispositions`, `asie-staging-admission-and-fixture`, `asie-reviewed-receipt-closeout`) have a load-bearing sequence. The reviewed receipt closeout is the gate before the staged build can be admitted, and the redaction cleanup is a compliance prerequisite before anything goes into a published receipt record. I'm going to start with `asie-reviewed-receipt-closeout` and work backward through the sequence to figure out what the receipt actually needs before I decide whether `asie-staging-admission-and-fixture` can follow in the same session.

### Secondary Work

**Draft the implementation plan for `horizontal-slice-hs186-decision-routing-tenant-context`.** I completed `hs186-inventory-route-decision-path` yesterday — that unit is done and the inventory is now frozen. The next unit in the planning pipeline is the implementation plan itself, and having the inventory in hand means I have the exact decision-routing queue contract to design against. The eight work units in this plan span decisions, docs, event, and idempotency domains — that breadth suggests the implementation plan needs to be sequenced deliberately rather than treated as a flat list.

### Maintenance

**Regenerate route health snapshot with `make sync-routes`.** The current snapshot is 33 days old across 3,447 routes. The route surface has changed substantially since then — multiple horizontal slices landed this week that touch webhook, admin, and queue endpoints. Stale route data means any route-health-adjacent work is navigating with an outdated map.

**Scope the `rd100v2-state-effects-warnings-wave` work before committing to it.** The react-doctor sprint has 321 State & Effects warnings outstanding outside the Phase 1 hotspots. Before touching that unit, I want to run a quick grep against the files I'm already modifying today to see whether any of them are in the warning set. If they are, I can address them inline rather than opening a separate pass.

**Draft the implementation plan for `quality-debt-bootstrap-artifacts`.** This directory is flagged as needing research before any work can start, and I haven't looked at it yet. A focused investigation session — reading whatever scaffolding exists, checking for adjacent planning artifacts — should be enough to decide whether it needs a full research spike or can move directly to planning.

**Check markdownlint findings against `dha-054` files before running a separate lint pass.** The 2 markdownlint issues in the current snapshot are in 1 file. If that file is in the email CDP cutover documentation I'm already touching for `dha-054-email-cdp-cutover-metadata-lint`, I can resolve the lint finding as part of the same change. If it's unrelated, it still takes less than five minutes to identify and fix directly in the file — that's faster than scheduling a dedicated pass.

### Parked

The `rd100v2-state-effects-warnings-wave` unit is parked as a standalone effort today. 321 warnings is a real number, but a wave that size benefits from a scoped entry strategy rather than an open-ended session. The maintenance item above covers the scoping work; the execution follows once I know which files are highest-leverage.

The `jest-coverage-report-ratchet-remediation` plan (12 units, starting with `jestcov-batch-preflight`) is not in today's focus because the PHP test suite is currently reporting 0% pass rate across all 1,583 tests. Running Jest coverage ratchet work while the PHP test environment is in that state creates a false baseline — any coverage metrics produced are measuring a broken environment, not actual coverage. The PHP test failure situation needs investigation before coverage ratcheting is meaningful. That investigation isn't scoped as a work unit today, but it's the actual blocker for the Jest work.

<!-- plan-unit-ids: asie-staging-admission-and-fixture,dha-041-development-setup-commands,dha-052-auth-waiver-frontmatter,dha-054-email-cdp-cutover-metadata-lint,rd100v2-state-effects-warnings-wave -->
<!-- SECTION: DAILY-PLAN END -->

<!-- Generated by dev-tracker build_today_plan.py -->
