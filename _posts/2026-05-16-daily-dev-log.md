---
layout: post
title: "Daily Dev Log - 2026-05-16"
date: 2026-05-16
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-05-16T13:24:36.190516+00:00 -->

## Today's Theme

I knocked out that digital-twin feature set yesterday - 25 items closed from boundary research through deployment readiness - but the security work I touched has me genuinely paranoid about what we've exposed over the years. The accidental-pint remediation is down to just two cohorts and they're both in sensitive areas that could break money flows if I rush them. What's actually driving my urgency though is this tenant isolation work that landed yesterday - the authorization gaps I found are keeping me up at night.

## The Main Work

**Fix the LoginHistory cross-tenant exposure vulnerability (acl-ct1-login-history-tenant-scope)** - This is a P0 security issue that I discovered yesterday and it's genuinely scary. The LoginHistory model is leaking data across tenant boundaries, which means admin users might be seeing login attempts from other customers. In a compliance audit, this kind of tenant isolation failure could sink the entire business. I need to add proper tenant scoping to the query builder and verify that the admin UI respects those boundaries.

**Remediate the Core Billing accidental Pint cohort (accidental-pint-core-billing)** - I've been avoiding this for weeks because billing code touches invoice generation and payment processing. Any formatting changes that introduce subtle arithmetic bugs or rounding errors could affect customer charges, and those problems don't surface until angry customers start calling about wrong bills. I'd rather spend the time to do this methodically than discover three months from now that we've been overcharging people due to a stray semicolon.

**Build the cross-tenant test helpers for HTTP-level validation (acl-m1-1-test-helpers)** - The authorization work is useless without proper test coverage, and I need helpers that can verify tenant isolation at the HTTP boundary. The existing Ship/Tests/CrossTenantTestCase probably has the foundation, but I need three specific helpers: one that asserts a request returns 403 when crossing tenant boundaries, one that validates data scoping, and one that checks authorization headers. Without these, I'm just hoping the security fixes actually work.

**Complete the Core ETL accidental Pint remediation (accidental-pint-core-etl)** - This closes out the formatting mess that's been haunting me. The ETL layer processes so much production data that I'm paranoid about introducing bugs in data transformation or pipeline orchestration. Better to finish this carefully than leave it half-done and risk corrupting our analytics or breaking downstream reporting that customers depend on.

## Housekeeping

**Regenerate the stale PHP test report (make test-fixed-batches-quick)** - The current results are 17 days old and I need fresh data to understand what's actually broken versus what got fixed recently. The 89% pass rate might be better now.

**Fix the single TypeScript error across 1 file** - This is probably a missing type import somewhere and should take five minutes to track down. Clean TypeScript builds make the frontend more reliable.

**Draft the production readiness gate inventory (prod-gate-inventory)** - The security vulnerabilities I found yesterday make me want to formalize our production checklist. This planning work connects to the tenant isolation fixes I'm already deep in.

**Update the codebase metrics (make codebase-metrics)** - These are 14 days stale and I'm curious if the recent cleanup work moved the needle on file counts or technical debt.

## Parked

The developer quickstart CI work is sitting there ready but the security issues feel more urgent right now. I'd rather have a secure system that's hard to set up than an easy-to-deploy system that leaks customer data. The billing remediation is scary enough that I don't want to split focus across too many sensitive areas at once.

<!-- plan-unit-ids: accidental-pint-core-etl,acl-m1-1-test-helpers,file-transfer-eligibility-characterize-interface,hs126-ci-smoke-dev-up,todoremed-p0-replace-template-boilerplate -->
<!-- SECTION: DAILY-PLAN END -->


<!-- SECTION: ACCOMPLISHED START -->
<!-- accomplished-generated: 2026-05-16T23:27:02.808081+00:00 -->

## Today's Update

Today was massive - I completely closed out the tenant isolation security initiative while simultaneously shipping two critical horizontal infrastructure slices and launching the trust manifest fabric. Fifty-nine completed tasks across five different feature areas, but it wasn't about the volume. It was about finally getting the security foundation solid enough to build on.

The tenant isolation work consumed most of my attention. I systematically worked through the B1 batch items - email provider credential validation, FinOps ETL pipeline, price catalogue endpoints, feature flags admin, and about ten other security-sensitive surfaces. Each one required careful policy binding to ensure tenant data never leaks across boundaries. The CT series (cross-tenant vulnerability fixes) were the scariest - login history was exposing all tenants, dashboard performance metrics were bleeding across accounts, and the entire erasure-audit family needed tenant scoping. I also completed three deepsec checkpoints after closing milestones M1, M2, and M3, which gave me confidence that the static analysis rules are actually catching violations.

The queue infrastructure work turned out to be more involved than expected. I built out the entire tenant-aware queue lane system - added the Redis connection alias, implemented the TenantLaneDispatcher, created the BulkJobBudget value object for throttling, and wired up middleware to ensure every async job runs in the correct tenant context. The hardest part was extending the Prometheus metrics to include tenant_id labels without breaking the existing dashboard queries. I also built a React admin partial for monitoring per-tenant queue depth, which should help with debugging when specific tenants start monopolizing worker capacity.

Parallel to that, I implemented the slow-query registry system from scratch. Added the database table, built a cache-backed sample buffer to avoid overwhelming the system with query events, and created a scheduled collector that snapshots the top-N slowest queries every hour. The cross-tenant integration test was particularly tricky - had to ensure that tenant A's slow queries don't appear in tenant B's admin dashboard. I'm not entirely happy with the retention job's performance characteristics yet, but deleting 30-day-old records shouldn't be a bottleneck.

The trust manifest fabric launch feels like a bigger deal than the task count suggests. I introduced the publication service, implemented the attestation issuer registry, and built out seven different public-safe projection endpoints. The capability catalog normalization was the most complex piece - taking raw MCP capability metadata and transforming it into something that external parties can actually parse and trust. This sets up the entire external transparency story, but I'm already seeing places where the projection logic is going to need refinement as we get real usage data.


<!-- Generated by dev-tracker publish_to_jekyll.py (AI mode) -->
<!-- accomplished-date: 2026-05-16 -->
<!-- unit-ids: acl-b1-09-provider-credential-validation,acl-p4-erasure-audit-anchoring-tenant-binding,acl-m1-1-test-helpers,acl-ct3-dashboard-performance-metrics,acl-b1-14-finops-etl,acl-p6-billing-invoices-account-binding,acl-m1-2-phpstan-authorize-rule,acl-ct1-login-history-tenant-scope,acl-b1-02-prices-by-sku,acl-b1-07-feature-flags,acl-b1-15-financial,acl-m3-deepsec-checkpoint,acl-p6-deployment-runtime-env-files,acl-ct2-erasure-audit-family,acl-m2-deepsec-checkpoint,acl-b1-01-currencies-regions-exchange-rates,acl-b1-03-tax-rules,acl-b1-04-product-controller,acl-b1-10-file-connectors,acl-b1-11-targeting,acl-b1-12-waitlist,acl-adr-authorization-tenancy-defaults,acl-p6-admin-api-contract-fresh-mfa,acl-m1-3-phpstan-belongs-to-account-rule,acl-m1-5-model-audit,acl-m1-6-route-audit,acl-b1-05-theme-studio,acl-b1-06-media-library,acl-b1-08-agent-registry,acl-b1-13-market-intelligence,acl-m1-4-phpstan-scope-bypass-rule,acl-m1-deepsec-checkpoint,acl-p6-admin-api-route-inventory,hs121-add-tenant-lane-config,hs125-registry-table-migration,hs121-bulk-job-budget-value-object,hs121-implement-tenant-lane-dispatcher,hs121-ensure-tenant-queue-lane-middleware,hs121-throttle-bulk-job-middleware,hs125-query-event-sample-buffer,hs125-scheduled-collector-command,hs121-tenant-queue-prometheus-labels,hs125-integration-test-cross-tenant,hs125-prometheus-alert-rule-fixture,hs125-admin-slow-query-partial,hs121-admin-queue-depth-partial,hs121-runbook-and-adr,hs125-retention-job,hs125-runbook-and-adr,hs125-n-plus-one-followup-scope,iai-phase1-mcp-analytics-summary-read,trust-manifest-fabric-publication-service,trust-manifest-fabric-attestation-issuer-registry,trust-manifest-fabric-capability-catalog-normalization,trust-manifest-fabric-agent-eval-status-projection,trust-manifest-fabric-provenance-manifest-projection,trust-manifest-fabric-ui-governance-projection,trust-manifest-fabric-compliance-manifest-projection,trust-manifest-fabric-operational-status-feed-projection -->

<!-- accomplished-unit-ids: acl-adr-authorization-tenancy-defaults,acl-b1-01-currencies-regions-exchange-rates,acl-b1-02-prices-by-sku,acl-b1-03-tax-rules,acl-b1-04-product-controller,acl-b1-05-theme-studio,acl-b1-06-media-library,acl-b1-07-feature-flags,acl-b1-08-agent-registry,acl-b1-09-provider-credential-validation,acl-b1-10-file-connectors,acl-b1-11-targeting,acl-b1-12-waitlist,acl-b1-13-market-intelligence,acl-b1-14-finops-etl,acl-b1-15-financial,acl-ct1-login-history-tenant-scope,acl-ct2-erasure-audit-family,acl-ct3-dashboard-performance-metrics,acl-m1-1-test-helpers,acl-m1-2-phpstan-authorize-rule,acl-m1-3-phpstan-belongs-to-account-rule,acl-m1-4-phpstan-scope-bypass-rule,acl-m1-5-model-audit,acl-m1-6-route-audit,acl-m1-deepsec-checkpoint,acl-m2-deepsec-checkpoint,acl-m3-deepsec-checkpoint,acl-p4-erasure-audit-anchoring-tenant-binding,acl-p6-admin-api-contract-fresh-mfa,acl-p6-admin-api-route-inventory,acl-p6-billing-invoices-account-binding,acl-p6-deployment-runtime-env-files,hs121-add-tenant-lane-config,hs121-admin-queue-depth-partial,hs121-bulk-job-budget-value-object,hs121-ensure-tenant-queue-lane-middleware,hs121-implement-tenant-lane-dispatcher,hs121-runbook-and-adr,hs121-tenant-queue-prometheus-labels,hs121-throttle-bulk-job-middleware,hs125-admin-slow-query-partial,hs125-integration-test-cross-tenant,hs125-n-plus-one-followup-scope,hs125-prometheus-alert-rule-fixture,hs125-query-event-sample-buffer,hs125-registry-table-migration,hs125-retention-job,hs125-runbook-and-adr,hs125-scheduled-collector-command,iai-phase1-mcp-analytics-summary-read,trust-manifest-fabric-agent-eval-status-projection,trust-manifest-fabric-attestation-issuer-registry,trust-manifest-fabric-capability-catalog-normalization,trust-manifest-fabric-compliance-manifest-projection,trust-manifest-fabric-operational-status-feed-projection,trust-manifest-fabric-provenance-manifest-projection,trust-manifest-fabric-publication-service,trust-manifest-fabric-ui-governance-projection -->
<!-- SECTION: ACCOMPLISHED END -->
<!-- Generated by dev-tracker build_today_plan.py -->
