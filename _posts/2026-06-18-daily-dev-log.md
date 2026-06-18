---
layout: post
title: "Daily Dev Log - 2026-06-18"
date: 2026-06-18
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-06-18T13:16:09.744339+00:00 -->

## Today's Plan

The consent boundary transition has been in active motion since Monday — all 12 items progressed yesterday but none are fully closed. Today is about converting that progress into completions.

### Main Focus

**Close out the consent boundary document and inventory items** — `consent-boundary-document-source-consumer-model`, `consent-boundary-inventory-routes`, and `consent-boundary-target-navigation-map` are the logical first three to land. The source-consumer model document is the conceptual anchor for everything downstream: without it written and committed, the route shell work and copy updates don't have a stable reference. I want this artifact done before I touch any route code, because "Consent Management owns consent state; Publishing Operations reads derived eligibility" is a decision that needs to be explicit, not implicit in file names and comments.

**Create the Publishing Operations route shell (`consent-boundary-publishing-route-shell`)** — Once the navigation map is settled, the route shell is the first concrete code change. The decision here is whether to create a new route file outright or rename an existing one. The old `/admin/consent/dashboard` is the incumbent, but carrying that name into Publishing Operations territory muddies the conceptual split permanently. I'd rather create a clean shell at the new path and handle the old URL with `consent-boundary-old-route-compatibility` as a redirect — that keeps the semantics honest. The two items pair naturally: shell first, redirect second.

**Work through `consent-boundary-audit-existing-permissions` and `consent-boundary-route-permission-tests`** — The audit needs to happen before the permission tests, and both need to happen before browser verification. I've been deferring the permission audit implicitly by doing documentation and copy work first, but once the route shell exists there's no reason not to immediately audit what authorization model it inherits. The tenant-scope question here is non-trivial — I need to verify that the Publishing Operations eligibility surface respects the same tenant isolation as the Consent Management source routes.

**Advance `cpdcp-authorship-classification-contract`** — Content provenance is 30% complete after yesterday's session, which landed migrations, models, tasks, enums, and a disclosure evaluator. The authorship classification contract is next in the ready queue and it's a genuine design decision point: the contract needs to define whether classification happens at write time (during content ingestion) or read time (during publication preflight). Writing it at ingestion means faster preflight but classification errors get baked into records. Read-time classification is slower but correctable. I don't have a settled answer yet.

### Secondary Work

**Begin `hubspot-conn-routes-file`** — Creating the `etl-hubspot-oauth.private.php` routes file is a self-contained task that doesn't require any decisions about the frontend token input or cross-tenant isolation tests. The HubSpot connection flow plan is one day old and at 0% — scaffolding the routes file now gives the feature set its first concrete artifact and makes the subsequent frontend and test items easier to sequence.

### Maintenance

**Regenerate the route health report** — The route health snapshot is six days old and showing a warning state against 3,167 routes. Given that the consent boundary transition is actively renaming and adding routes, I don't trust a six-day-old baseline. Running the route health make target now gives me a current reference before I make structural route changes today.

**Fix Markdownlint issues in consent boundary planning files** — The planning directory files I'm touching today likely contribute to the 175 Markdownlint issues across 11 files. While I have those files open for content edits, fixing heading hierarchy and trailing whitespace costs nothing and keeps the documentation artifacts clean.

**Draft implementation plan for `admin-visual-standardization` → `avs-001`** — This is next in the ready queue and I touched admin visual standardization yesterday. The `avs-001` work unit documents the visual drift inventory and target admin grammar — that artifact is prerequisite to all the tab standardization and error-state surface work in the plan. Drafting the implementation plan now while the admin UI changes from yesterday are fresh in memory is better than reconstructing context later.

**Check the 50 PHP test failures for environment causes** — The test suite is showing 0 of 50 passing. Before treating that as 50 real regressions, I want to run a subset manually to determine whether this is a database connection issue, a missing env variable, or actual test breakage. The answer changes the response entirely: environment problem gets fixed once, real regressions get triaged individually.

### Parked

**`phpstan-baseline-freeze-2026-06-14`** and the other PHPStan remediation items stay parked today. They've been in-progress for several days without closing — the consent boundary work is higher leverage right now and PHPStan remediation is a context-switch that breaks the flow of route and navigation work. I'll return to it once the boundary transition items start landing.

**`hubspot-conn-test-cross-tenant` and `hubspot-conn-fe-private-app-field`** are waiting on the routes file. The cross-tenant isolation test needs a route to test, and the frontend token input needs an endpoint to submit against. Sequencing is the blocker, not priority.

**`avs-003`, `avs-005`, and `avs-009`** are parked pending `avs-001`. Standardizing tabs and error states without a documented target grammar to conform to risks doing that work twice.

<!-- plan-unit-ids: avs-001,consent-boundary-inventory-routes,cpdcp-pageeditor-adapter,cpdcp-takedown-intake-action,hubspot-conn-config-etl-php,hubspot-conn-fe-mode-toggle,phpstan-baseline-freeze-2026-06-14,todoremed-p0-replace-template-boilerplate -->
<!-- SECTION: DAILY-PLAN END -->

<!-- Generated by dev-tracker build_today_plan.py -->
