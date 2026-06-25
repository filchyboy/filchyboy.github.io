---
layout: post
title: "Daily Dev Log - 2026-06-24"
date: 2026-06-24
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-06-24T13:21:37.663425+00:00 -->

## Today's Plan

Wednesday. Yesterday turned into a broad sweep — model governance plane, enforcement intelligence, admin accessibility sprint, decision policy hotfix — all merged. The three feature sets marked active this morning (tenant-trust, deferred-accessibility-test-coverage, deferred-security-authorization-follow-up) all got touches yesterday too, which tells me the priority ordering is right. Today I want to execute rather than scope.

### Main Focus

**Begin the tenant-trust isolation verification items, starting with `tt-iso-schema-contract-check`** — The tenant-trust plan is 225 days old at 0% overall completion across 68 tracker items. That's a long runway with no landings. The five ready items are all Phase 1 — the Tenant Isolation Verification Framework — and they're sequenced correctly: schema contract checks come before the CI command, the report schema, the classifier, and the bypass inventory. `tt-iso-schema-contract-check` specifically integrates `BelongsToAccount` schema-contract checks, which is a concrete, bounded piece of work: find the query paths that skip tenant scoping, verify the `BelongsToAccount` contract applies, and document what passes and what doesn't. The bypass inventory (`tt-iso-scope-bypass-inventory`) is downstream — I can't credibly inventory bypass call sites until I know what the contract looks like. Starting with the schema check gives me the reference I need for everything else in Phase 1.

**Work through `hs97-api-contract-hardening` in deferred-security-authorization-follow-up** — This item standardizes the 403 contract follow-up from horizontal slice hs97. The authorization work that landed yesterday (enforcement-intelligence, admin-ui accessibility) touched adjacent surfaces, and the 403 contract question is one I'd rather answer while those code paths are fresh. The plan is at 0/3 complete and has been ready since June 19. The risk of leaving 403 response shapes unstandardized is that we end up with clients branching on different error shapes — some seeing `{"message": "Forbidden"}` and others seeing a structured policy-denial envelope. That inconsistency is the kind of thing that looks fine until it isn't.

**Pick up the next PHPStan remediation wave** — I've had heavy focus on the phpstan-baseline-remediation this week, and Phase 2 (high-volume type-shape repairs) is next. The tracker shows `phpstan-type-shape-ship-compliance` and `phpstan-type-shape-mcp-etl` as the leading items. At 2,454 errors at level 9, I'm not going to close this in a day, but the sweep harness has already processed 375 of 15,593 harness files with 333 remediated. The remediation pattern is established — it's execution now, not design. The type-shape findings in Ship and Compliance are the highest volume category, so that's where the error count moves fastest per hour of work.

**Complete `tw-p8-accessibility-audit` — the pa11y audit on all migrated pages** — The admin accessibility sprint landed a significant batch yesterday (aria-busy resets, focus/focus-visible styles, keyboard navigation, Blade view migrations). Running the pa11y audit now, immediately after those changes land, is the right verification step rather than leaving it for later when the changes are harder to trace. The `deferred-accessibility-test-coverage` plan has 24 tracker items at 0% complete, and the audit is the logical first one — it produces the evidence that either confirms the sprint's work or surfaces the gaps that need follow-up.

### Secondary Work

**Draft the scope for `hs97-observability-instrumentation`** — The second item in deferred-security-authorization-follow-up covers authorization denial telemetry and rollout-mode wiring. I'm not sure yet whether the telemetry belongs at the middleware layer or in the policy resolution path — the middleware approach instruments every request uniformly, but policy-layer instrumentation gives richer context about which rule fired. That's a real trade-off worth thinking through before writing code. If `hs97-api-contract-hardening` completes cleanly, I can use the remaining time to at least write out the instrumentation points so the actual implementation session isn't starting cold.

### Maintenance

**Refresh the PHP test report** — The current test snapshot is 9 days old with 0 of 50 passing. That 0% pass rate against a 9-day-old snapshot is almost certainly not the current state of things given how much has merged this week. Running `make test-fixed-batches-quick` gives me an actual number to work with rather than a stale one that looks alarming.

**Refresh route health** — Route health is 12 days old at 3,167 routes with a warning status. That's the oldest stale report in the set, and given the volume of merges this week, the route count has almost certainly changed. Running `make sync-routes` is a one-command refresh.

**Update codebase metrics** — At 9 days old and 30,498 files / 5,819,307 LOC, the codebase metrics are due for a refresh. Running `make codebase-metrics` takes a few minutes and keeps the baseline accurate for the planning pipeline calculations.

**Draft the implementation plan for `crypto-prov-integration-mutations-signing-plan`** — The cryptographic provenance integration mutations plan has one unit ready and sits in the planning pipeline with domain tags across cryptographic-provenance, integrations, mcp, and security. The deferred-cryptographic-provenance-follow-on-planning work I completed yesterday (including `crypto-prov-follow-on-kms-plan`) provides direct context for what the signing plan needs to say. The KMS productionization planning is done; the next concrete step is scoping how integration mutations get signed.

### Parked

**`tt-iso-resource-classifier` and `tt-iso-report-schema`** — These are Phase 1 items in tenant-trust, but they're downstream of the schema contract check and the CI command. Starting the classifier before the contract check is settled would mean building a scanner that might be classifying against the wrong criteria. Sequencing matters here.

**`boundary-governance-tooling-sprint` and `security-prod-boundary-sprint`** — Both are in the planning pipeline with substantial unit counts (12 and 27 respectively), but neither has had recent activity and I don't have enough loaded on those domains today to do the scoping work justice. The security sprint in particular has crypto-erasure, domain-auth, and domain-billing — that's a broad surface for a context switch mid-week.

**ESLint warnings (1,141 total, 176 fixable)** — The ESLint report is current and the warning count is real remediation work, not a stale snapshot. Addressing it properly means reviewing the 176 fixable warnings file by file in areas I'm actually touching — not running a broad auto-fix. I'll pick at this as I work through the accessibility and authorization code today, but it's not a standalone session item.

<!-- plan-unit-ids: phpstan-report-visibility-ratchet,phpstan-type-shape-mcp-etl,phpstan-type-shape-ship-compliance,tw-p8-accessibility-audit -->
<!-- SECTION: DAILY-PLAN END -->


<!-- SECTION: ACCOMPLISHED START -->
<!-- accomplished-generated: 2026-06-25T03:40:23.027571+00:00 -->

## Today's Update

Today was the content provenance deep dive I've been building toward since the initial schema work on the 17th. The CPDCP module — Content Provenance, Disclosure, and Compliance Policy — went from interface contracts to working API endpoints, MCP tools, and enforcement integration in a single session. That's a lot of ground, and the sequencing mattered.

The contracts came first, deliberately. Before writing any implementation, I defined the module interface contract, the Regulatory Rule Authority contract, the authorship classification contract, the publication preflight decision contract, and both the REST API and MCP tool contracts. Six distinct interface definitions before a single action was written. The reason for that order: the disclosure evaluator, the publishing preflight integration, and the render restriction guard all need to agree on what a provenance record looks like and what enforcement decisions it can produce. Establishing those shapes upfront meant the downstream implementation had stable types to work against rather than inferring them from the first consumer that happened to get written. Whether that's always the right call is a genuine question — contracts-first adds friction early in exchange for coherence later, and I won't know if the trade held until the PageEditor and Publishing adapters are exercised under realistic content flows.

The implementation sequence moved from adapters inward to enforcement outward. The `PageEditor` ChangeSet provenance adapter and the Publishing `PageVersion` provenance adapter are the intake points — they're responsible for creating or updating provenance records as content moves through the editing and publishing lifecycle. From there, CPDCP integrates into the publishing preflight check, which means a content item can now be blocked from promotion if required enforcement hasn't cleared. The render restriction guard sits at the other end: public rendering for restricted artifacts gets blocked before output. The takedown path — intake action, restriction action, and tests for both — completes the enforcement surface. Together these three enforcement points cover the full lifecycle: pre-publication, post-publication, and forced retraction.

The REST and MCP layers went in after the core enforcement was testable. The REST side covers four endpoint groups: provenance records, disclosure evaluations, regulatory regimes, and takedown notices. The MCP tools are read-mostly by design — `provenance.lookup`, `provenance.lineage`, and `provenance.disclosures` — which reflects a deliberate choice to keep write operations in the REST surface rather than exposing them through the tool interface. That boundary is worth watching; if an AI-assisted workflow needs to initiate a takedown or trigger a disclosure evaluation, the read-only MCP contract will need revisiting. I documented that as a quality gate item rather than deferring it silently.

The day also cleared deferred staging verification for the Docker environment workflows — the staging pipeline passes and the end-to-end verification artifact is recorded — and moved through four accessibility documentation items: the waiver workflow, the reusable a11y test template utility, threshold semantics and strict mode documentation, and an update to `accessibility-kpi-system.md` with the mapping methodology. The new ADRs for data element control and compliance evidence landed alongside a provenance boundary enforcement task that closes the loop on the content provenance isolation work. Phase 1 quality evidence is recorded. The CPDCP feature set is, at minimum, structurally complete — what it isn't yet is exercised under realistic tenant content flows, which is where the real validation will come from.

---
<!-- Generated by dev-tracker publish_to_jekyll.py (AI mode) -->
<!-- accomplished-date: 2026-06-24 -->
<!-- unit-ids: dagger-manifest-verify-staging,synthetic-data-e2e-verification-artifact,a11y-docs-waiver-process,a11y-tests-helper-utility,a11y-docs-strict-mode,a11y-docs-kpi-system-update,cpdcp-module-interface-contract,cpdcp-regulatory-authority-contract,cpdcp-authorship-classification-contract,cpdcp-publication-preflight-contract,cpdcp-rest-api-contract,cpdcp-mcp-tool-contract,cpdcp-quality-gate-matrix,cpdcp-pageeditor-adapter,cpdcp-publishing-pageversion-adapter,cpdcp-publishing-preflight-integration,cpdcp-publishing-promotion-block,cpdcp-render-restriction-guard,cpdcp-takedown-intake-action,cpdcp-takedown-restriction-action,cpdcp-takedown-tests,cpdcp-rest-provenance-endpoints,cpdcp-rest-disclosure-endpoints,cpdcp-rest-regime-endpoints,cpdcp-rest-takedown-endpoints,cpdcp-api-tests,cpdcp-mcp-lookup-tool,cpdcp-mcp-lineage-tool,cpdcp-mcp-disclosures-tool,cpdcp-mcp-tests,cpdcp-phase1-quality-evidence,cpdcp-authorship-enums,cpdcp-provenance-record-migration,cpdcp-attribution-migration,cpdcp-disclosure-evaluation-migration,cpdcp-tenant-policy-migration,cpdcp-regulatory-regime-migration,cpdcp-regulatory-rule-migration,cpdcp-takedown-notice-migration,cpdcp-provenance-models,cpdcp-regulatory-models,cpdcp-upsert-record-task,cpdcp-record-attribution-task,cpdcp-query-records-task,cpdcp-regime-rule-service,cpdcp-disclosure-evaluator-task,cpdcp-disclosure-evaluator-tests,new-adrs-new-adrs-data-element-control,provenance-enforce-content-provenance-boundaries -->

<!-- accomplished-unit-ids: a11y-docs-kpi-system-update,a11y-docs-strict-mode,a11y-docs-waiver-process,a11y-tests-helper-utility,cpdcp-api-tests,cpdcp-attribution-migration,cpdcp-authorship-classification-contract,cpdcp-authorship-enums,cpdcp-disclosure-evaluation-migration,cpdcp-disclosure-evaluator-task,cpdcp-disclosure-evaluator-tests,cpdcp-mcp-disclosures-tool,cpdcp-mcp-lineage-tool,cpdcp-mcp-lookup-tool,cpdcp-mcp-tests,cpdcp-mcp-tool-contract,cpdcp-module-interface-contract,cpdcp-pageeditor-adapter,cpdcp-phase1-quality-evidence,cpdcp-provenance-models,cpdcp-provenance-record-migration,cpdcp-publication-preflight-contract,cpdcp-publishing-pageversion-adapter,cpdcp-publishing-preflight-integration,cpdcp-publishing-promotion-block,cpdcp-quality-gate-matrix,cpdcp-query-records-task,cpdcp-record-attribution-task,cpdcp-regime-rule-service,cpdcp-regulatory-authority-contract,cpdcp-regulatory-models,cpdcp-regulatory-regime-migration,cpdcp-regulatory-rule-migration,cpdcp-render-restriction-guard,cpdcp-rest-api-contract,cpdcp-rest-disclosure-endpoints,cpdcp-rest-provenance-endpoints,cpdcp-rest-regime-endpoints,cpdcp-rest-takedown-endpoints,cpdcp-takedown-intake-action,cpdcp-takedown-notice-migration,cpdcp-takedown-restriction-action,cpdcp-takedown-tests,cpdcp-tenant-policy-migration,cpdcp-upsert-record-task,dagger-manifest-verify-staging,new-adrs-new-adrs-data-element-control,provenance-enforce-content-provenance-boundaries,synthetic-data-e2e-verification-artifact -->
<!-- SECTION: ACCOMPLISHED END -->
<!-- Generated by dev-tracker build_today_plan.py -->
