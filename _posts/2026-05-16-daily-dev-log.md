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
<!-- accomplished-generated: 2026-05-17T02:45:19.762006+00:00 -->
<!-- accomplished-updated: 2026-05-17T02:45:19.762006+00:00 -->

* Completed 88 tasks today on the Colossalistic Platform project.

## What I Built

### archive-react-doctor
* Archive react doctor followup sprint

### data
* Update detectedAt timestamp in tech.json

### enhance-assertion
* Enhance assertion for unauthorized access in LicenseInventoryApiControllerTest

### file-transfer-eligibility-deepening
* Characterize the current Transfer Eligibility Interface
* Run scoped quality gates for File Transfer eligibility
* Add characterization tests for eligibility outcomes
* Consolidate shallow eligibility rule Tasks behind the Module
* Document the deepened Transfer Eligibility Interface
* Close out planning evidence and follow-ups

### horizontal-slice-hs121-tenant-aware-queue-lanes
* Add tenant-lane Redis connection alias to config/queue.php
* Add Ship/Queue/BulkJobBudget value object
* Implement Ship/Queue/TenantLaneDispatcher and bind in AppServiceProvider
* Wire EnsureTenantQueueLane middleware on every async entry point
* Implement Ship/Queue/Middleware/ThrottleBulkJob enforcing BulkJobBudget
* Extend HS93 emitter with tenant_id label for queue counters
* Build admin React partial + Storybook for per-tenant queue-depth
* Publish queue-tenant-lanes runbook + ADR

### horizontal-slice-hs125-slow-query-registry-prometheus-dashboard
* Add slow_query_registry table migration
* Add cache-backed bounded slow-query event sample buffer
* Scheduled collector command snapshotting top-N slow queries
* Cross-tenant integration test for slow-query registry
* Prometheus alert rule fixture for coarse database latency budget
* Blade admin slow-query triage section
* Retention job: delete slow_query_registry rows older than 30 days
* Publish slow-query registry runbook + narrow ADR
* Capture follow-up scope for N+1 static-analysis advisory rollout

### improve-data-handling
* Improve data handling and validation in various services and requests

### internal-agent-integration
* Phase 1: MCP bounded analytics summary (read:analytics.summary)

### login-api
* Update login API endpoint and add redirect option in AuthService tests

### plans
* Add retroactive planning documentation for  data handling, enhance assertion, and trust manifest

### react-doctor-100-followup-sprint
* Audit dead-code and React 19 diagnostics before broad cleanup
* Drive the exact root React Doctor command to 100 out of 100
* Reduce the next bounded state-management bucket
* Reduce the remaining hydration mismatch and Intl recreation bucket
* Clear the next generic-handler and quick-win architecture bucket
* Archive the sprint planning directory once the score target is actually met
* Fix current root React Doctor errors before warning remediation

### record-react-doctor
* Record react doctor followup archive evidence

### sec-acl-tenant-isolation-20260515
* B1-09 Email provider credential validation (P1)
* P4 B-1: Bind anchoring-status queries to authenticated tenant
* P7 D-1: Harden load-testing-staging workflow_dispatch inputs
* M1.1 Extend Ship/Tests/CrossTenantTestCase with 3 HTTP-level helpers
* CT-3 Dashboard performance metrics leak across tenants (P0)
* B1-14 FinOps ETL pipeline + jobs (P1)
* P6 C: Bind getCustomerInvoices to BillingAccountPolicy hierarchy
* M1.2 PHPStan rule: FormRequest::authorize() must not return true / null-check
* CT-1 LoginHistory exposes all tenants (P0)
* B1-02 PriceCatalogue: /prices/{sku} POST/PUT (P1)
* B1-07 Feature flags admin (P1)
* B1-15 /api/financial/* (P1)
* Deepsec checkpoint after M3 close (delta run 2026-05-16)
* P6 D-NEW: Move staging/production deploy secrets to Runtime Env Files
* P7 B-1: Bind plan-change proration to server catalog economics
* CT-2 Erasure-audit family — ledger, anchors, Merkle proof, suppression (P0)
* Deepsec checkpoint after M2 close
* B1-01 PriceCatalogue: currencies, regions, exchange rates (P1)
* B1-03 PriceCatalogue: /admin/tax-rules (P1)
* B1-04 ProductController store/update/destroy (P1)
* B1-10 File transfer connectors (P1)
* B1-11 Marketing targeting overlap + validation (P1)
* B1-12 Waitlist admin (P1)
* ADR: Authorization and tenancy defaults
* P6 MFA-1..MFA-5: Admin API Contract with Fresh MFA Proof
* P6 checkpoint: verify run-3 HIGH remediation
* M1.3 PHPStan rule: tenant-scoped models must use BelongsToAccount
* M1.5 Audit artifact: artifacts/belongs-to-account-model-audit.md
* M1.6 Audit artifact: artifacts/route-private-php-authorization-audit.md
* B1-05 Theme Studio (P1)
* B1-06 Media library (P1)
* B1-08 Agent registry (P1)
* B1-13 Market intelligence admin (P1)
* P7 B-3/C-1: Enforce capability-manifest permissions on admin APIs
* P7 B-2: Remove or gate legacy feature-flag WEB mutations
* P7 C-2: Prevent BaseApiClient auth headers on absolute cross-origin URLs
* M1.4 PHPStan rule: scope bypass requires super-admin guard or justification comment
* Deepsec checkpoint after M1 close
* P6 follow-up: classify remaining admin-ish JSON routes

### trust-manifest
* Add Trust Manifest Fabric Implementation Checklist, Plan, and Ticket Details

### trust-manifest-fabric
* Create authority source map for trust manifest projections
* Prepare draft ATM schema contribution for governance artifacts and third-party attestations
* Introduce Trust Manifest Publication Service
* Implement Trust-owned Attestation Issuer Registry
* Normalize MCP capability metadata into a public capability catalog
* Publish public-safe AgentEval evaluation status projection
* Publish public-safe provenance manifest projection
* Publish public-safe UI governance projection
* Publish public-safe compliance manifest projection
* Publish first-party operational status feed

## Notes

* Completed 88 work unit(s)
* Archived 2 previously completed unit(s)
* Item adherence: 40% (2/5 focus items)
* Feature set adherence: 40% (2/5 planned feature sets had work)
* Weighted adherence: 290% (with partial credit)
* Untracked activity: 51 commit(s) not mapped to any feature set


<!-- Generated by dev-tracker publish_to_jekyll.py -->
<!-- accomplished-date: 2026-05-16 -->
<!-- unit-ids: acl-b1-09-provider-credential-validation,acl-p4-erasure-audit-anchoring-tenant-binding,acl-p7-load-testing-staging-dispatch-input-hardening,acl-m1-1-test-helpers,acl-ct3-dashboard-performance-metrics,acl-b1-14-finops-etl,acl-p6-billing-invoices-account-binding,acl-m1-2-phpstan-authorize-rule,acl-ct1-login-history-tenant-scope,acl-b1-02-prices-by-sku,acl-b1-07-feature-flags,acl-b1-15-financial,acl-m3-deepsec-checkpoint,acl-p6-deployment-runtime-env-files,acl-p7-plan-change-proration-catalog-binding,acl-ct2-erasure-audit-family,acl-m2-deepsec-checkpoint,acl-b1-01-currencies-regions-exchange-rates,acl-b1-03-tax-rules,acl-b1-04-product-controller,acl-b1-10-file-connectors,acl-b1-11-targeting,acl-b1-12-waitlist,acl-adr-authorization-tenancy-defaults,acl-p6-admin-api-contract-fresh-mfa,acl-p6-deepsec-run3-checkpoint,acl-m1-3-phpstan-belongs-to-account-rule,acl-m1-5-model-audit,acl-m1-6-route-audit,acl-b1-05-theme-studio,acl-b1-06-media-library,acl-b1-08-agent-registry,acl-b1-13-market-intelligence,acl-p7-capability-manifest-permission-enforcement,acl-p7-feature-flags-web-route-cleanup,acl-p7-base-api-client-same-origin-auth,acl-m1-4-phpstan-scope-bypass-rule,acl-m1-deepsec-checkpoint,acl-p6-admin-api-route-inventory,rd100-audit-dead-code-and-react19-buckets,file-transfer-eligibility-characterize-interface,hs121-add-tenant-lane-config,file-transfer-eligibility-quality-gates,rd100-close-root-score-gap,hs125-registry-table-migration,rd100-finish-state-bucket-wave,file-transfer-eligibility-characterization-tests,hs121-bulk-job-budget-value-object,file-transfer-eligibility-deepen-module,hs121-implement-tenant-lane-dispatcher,hs121-ensure-tenant-queue-lane-middleware,hs121-throttle-bulk-job-middleware,hs125-query-event-sample-buffer,rd100-finish-hydration-and-intl-wave,hs125-scheduled-collector-command,hs121-tenant-queue-prometheus-labels,hs125-integration-test-cross-tenant,hs125-prometheus-alert-rule-fixture,rd100-finish-generic-handler-wave,hs125-admin-slow-query-partial,rd100-archive-sprint-plan,file-transfer-eligibility-document-interface,hs121-admin-queue-depth-partial,file-transfer-eligibility-closeout,hs121-runbook-and-adr,hs125-retention-job,hs125-runbook-and-adr,hs125-n-plus-one-followup-scope,iai-phase1-mcp-analytics-summary-read,archive-react-doctor-archive-react-doctor-followup-sprint,improve-data-handling-improve-data-handling-validation-various,login-api-login-api-endpoint-redirect-option,plans-retroactive-planning-documentation-data-handling,record-react-doctor-record-react-doctor-followup-archive,trust-manifest-trust-manifest-fabric-implementation-checklist,trust-manifest-fabric-authority-source-map,trust-manifest-fabric-atm-schema-contribution,trust-manifest-fabric-publication-service,trust-manifest-fabric-attestation-issuer-registry,trust-manifest-fabric-capability-catalog-normalization,trust-manifest-fabric-agent-eval-status-projection,trust-manifest-fabric-provenance-manifest-projection,trust-manifest-fabric-ui-governance-projection,trust-manifest-fabric-compliance-manifest-projection,trust-manifest-fabric-operational-status-feed-projection,rd100-fix-root-react-doctor-errors,data-detectedat-timestamp-tech-json,enhance-assertion-enhance-assertion-unauthorized-access-licenseinventoryapicontrollertest -->

<!-- accomplished-unit-ids: acl-adr-authorization-tenancy-defaults,acl-b1-01-currencies-regions-exchange-rates,acl-b1-02-prices-by-sku,acl-b1-03-tax-rules,acl-b1-04-product-controller,acl-b1-05-theme-studio,acl-b1-06-media-library,acl-b1-07-feature-flags,acl-b1-08-agent-registry,acl-b1-09-provider-credential-validation,acl-b1-10-file-connectors,acl-b1-11-targeting,acl-b1-12-waitlist,acl-b1-13-market-intelligence,acl-b1-14-finops-etl,acl-b1-15-financial,acl-ct1-login-history-tenant-scope,acl-ct2-erasure-audit-family,acl-ct3-dashboard-performance-metrics,acl-m1-1-test-helpers,acl-m1-2-phpstan-authorize-rule,acl-m1-3-phpstan-belongs-to-account-rule,acl-m1-4-phpstan-scope-bypass-rule,acl-m1-5-model-audit,acl-m1-6-route-audit,acl-m1-deepsec-checkpoint,acl-m2-deepsec-checkpoint,acl-m3-deepsec-checkpoint,acl-p4-erasure-audit-anchoring-tenant-binding,acl-p6-admin-api-contract-fresh-mfa,acl-p6-admin-api-route-inventory,acl-p6-billing-invoices-account-binding,acl-p6-deepsec-run3-checkpoint,acl-p6-deployment-runtime-env-files,acl-p7-base-api-client-same-origin-auth,acl-p7-capability-manifest-permission-enforcement,acl-p7-feature-flags-web-route-cleanup,acl-p7-load-testing-staging-dispatch-input-hardening,acl-p7-plan-change-proration-catalog-binding,archive-react-doctor-archive-react-doctor-followup-sprint,data-detectedat-timestamp-tech-json,enhance-assertion-enhance-assertion-unauthorized-access-licenseinventoryapicontrollertest,file-transfer-eligibility-characterization-tests,file-transfer-eligibility-characterize-interface,file-transfer-eligibility-closeout,file-transfer-eligibility-deepen-module,file-transfer-eligibility-document-interface,file-transfer-eligibility-quality-gates,hs121-add-tenant-lane-config,hs121-admin-queue-depth-partial,hs121-bulk-job-budget-value-object,hs121-ensure-tenant-queue-lane-middleware,hs121-implement-tenant-lane-dispatcher,hs121-runbook-and-adr,hs121-tenant-queue-prometheus-labels,hs121-throttle-bulk-job-middleware,hs125-admin-slow-query-partial,hs125-integration-test-cross-tenant,hs125-n-plus-one-followup-scope,hs125-prometheus-alert-rule-fixture,hs125-query-event-sample-buffer,hs125-registry-table-migration,hs125-retention-job,hs125-runbook-and-adr,hs125-scheduled-collector-command,iai-phase1-mcp-analytics-summary-read,improve-data-handling-improve-data-handling-validation-various,login-api-login-api-endpoint-redirect-option,plans-retroactive-planning-documentation-data-handling,rd100-archive-sprint-plan,rd100-audit-dead-code-and-react19-buckets,rd100-close-root-score-gap,rd100-finish-generic-handler-wave,rd100-finish-hydration-and-intl-wave,rd100-finish-state-bucket-wave,rd100-fix-root-react-doctor-errors,record-react-doctor-record-react-doctor-followup-archive,trust-manifest-fabric-agent-eval-status-projection,trust-manifest-fabric-atm-schema-contribution,trust-manifest-fabric-attestation-issuer-registry,trust-manifest-fabric-authority-source-map,trust-manifest-fabric-capability-catalog-normalization,trust-manifest-fabric-compliance-manifest-projection,trust-manifest-fabric-operational-status-feed-projection,trust-manifest-fabric-provenance-manifest-projection,trust-manifest-fabric-publication-service,trust-manifest-fabric-ui-governance-projection,trust-manifest-trust-manifest-fabric-implementation-checklist -->
<!-- SECTION: ACCOMPLISHED END -->
<!-- Generated by dev-tracker build_today_plan.py -->
