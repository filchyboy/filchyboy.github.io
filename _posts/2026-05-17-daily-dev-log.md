---
layout: post
title: "Daily Dev Log - 2026-05-17"
date: 2026-05-17
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-05-17T13:26:06.409447+00:00 -->

## Today's Theme

The security isolation work has consumed my weekend brain - I wrapped up 39 items yesterday in the tenant ACL feature set, but finding those cross-tenant data leaks is keeping me genuinely paranoid about production. The accidental-pint work that's been haunting me for weeks is finally down to two cohorts, and I'm terrified the billing one will surface money math bugs if I rush it. What's really pulling at me though is this fresh security work I touched in the last 24 hours - eight more tenant isolation items that feel urgent after discovering how exposed we've been.

## The Main Work

**Bind erasure-ledger filters to authenticated tenant context (acl-p4-erasure-ledger-tenant-filter)** - This is eating at me because erasure requests are compliance-critical and any cross-tenant data exposure here could violate GDPR in ways that destroy the business. The erasure ledger probably has unguarded queries that let tenant A see tenant B's deletion requests, which is exactly the kind of violation that regulators love to fine into oblivion. I need to add proper tenant scoping to the query builder before this becomes a regulatory nightmare.

**Complete the Core Billing accidental Pint cohort (accidental-pint-core-billing)** - I've been circling this for two weeks because billing code touches invoice generation and payment processing. Any Pint formatting changes that introduce subtle arithmetic bugs could affect customer charges, and those problems don't surface until three months later when customers call about wrong bills. The ETL cohort can wait - money math errors are career-ending mistakes that I'd rather prevent than explain to angry customers.

**Generate Merkle proof generation with tenant binding (acl-p4-merkle-proof-tenant-filter)** - The cryptographic proof system is probably leaking verification data across tenant boundaries, which breaks the entire trust model. If tenant A can request Merkle proofs for tenant B's transactions, our audit trail is fundamentally compromised. This touches the core integrity guarantees of the platform, so any delay here undermines customer trust in ways that are hard to recover from.

**Build suppression-list search with authenticated tenant scope (acl-p4-suppression-search-tenant-filter)** - Marketing suppression lists are another cross-tenant landmine - if tenant A's suppressed emails leak into tenant B's campaigns, that's both a privacy violation and a compliance failure. The search functionality probably has unguarded queries that need proper tenant filtering before someone accidentally sends marketing emails to opted-out users from other accounts.

## Housekeeping

**Regenerate the 18-day-old PHP test results (make test-fixed-batches-quick)** - The current 89% pass rate is ancient data that doesn't reflect any of the security work I've been doing. Fresh test results will either confirm the codebase is stable or surface regressions I need to address before they compound.

**Complete the planning baseline for tenant isolation phase tracking** - I need to draft the implementation plan for the ready-to-start sec-acl-tenant-isolation work since I'm already deep in this domain. The 62 work units need proper sequencing and the admin-api domain tags suggest this touches sensitive surfaces that require careful orchestration.

**Fix markdown violations in the 8 files flagged by markdownlint** - Since I'm updating security documentation as part of the ACL work, might as well clean up the 33 lint issues. Consistent documentation formatting makes the compliance audit trail more professional.

## Parked

The todo-remediation work sits at 68 units ready to implement, but security vulnerabilities trump code cleanup. The horizontal slice for developer quickstart is 75% complete but needs CI validation - that can wait until the tenant isolation gaps are sealed. I'm deliberately avoiding the production-readiness checklist because discovering more compliance gaps right now would be overwhelming when I'm already drowning in authorization fixes.

<!-- plan-unit-ids: accidental-pint-core-billing,acl-p4-erasure-ledger-tenant-filter,acl-p4-merkle-proof-tenant-filter,hs126-ci-smoke-dev-up,todoremed-p0-replace-template-boilerplate -->
<!-- SECTION: DAILY-PLAN END -->


<!-- SECTION: ACCOMPLISHED START -->
<!-- accomplished-generated: 2026-05-18T01:38:36.512582+00:00 -->

## Today's Update

This was one of those rare days where everything clicked - I managed to close out four major workstreams that have been consuming my attention for weeks. The security audit work, migration squashing, React Doctor remediation, and a sixth security scan followup all reached completion points simultaneously.

The tenant isolation security work finally wrapped up after weeks of systematic auditing. I finished binding the last few data access points to authenticated tenants - erasure ledger filters, Merkle proof generation, and suppression-list searches all now properly scope to the requesting tenant instead of leaking data across boundaries. The financial admin surfaces were particularly tricky because they had some legacy bypass logic that I had to carefully remove without breaking the legitimate admin workflows. I also added proper permission gates to a bunch of endpoints that were only protected by middleware, which was concerning. The Scribe documentation XSS issue got patched too - turns out the Try-It-Out feature was rendering unsanitized debug output, which is exactly the kind of thing security scanners love to flag.

The migration squashing project turned into a bigger undertaking than expected. I started by auditing all our open branches to make sure no old migrations would resurrect after the squash, then did a clean database rebuild to establish the canonical state. The actual squashing involved regenerating the MySQL schema dump, stripping out some stray DEFINER clauses, and removing the loadMigrationsFrom() calls from four Porto service providers. But the real work was building the tooling around it - I created equivalence diff scripts, resurrection guards, and location validators so future squashes won't be such a manual process. The gotcha that ate most of my time was a duplicate-row bug in the squashing script that took way too long to track down.

React Doctor finally hit 100/100, which has been a goal for months. I worked through the remaining state management issues, hydration mismatches, and accessibility warnings in focused waves. The dead code cleanup revealed some interesting architectural debt - we had components that were imported but never rendered, and handlers that were defined but never called. The accessibility work was actually educational; I learned about some ARIA patterns I hadn't encountered before. Now I need to figure out how to maintain this score as the codebase evolves, since React Doctor tends to drift downward without active attention.

Between all this, I knocked out the sixth security scan followup work - production Docker compose boundaries, k6 test vendoring, and some dashboard cache scoping issues. It's satisfying to have these long-running streams finally converge and close out on the same day. Tomorrow I can shift focus to some of the feature development work that's been waiting in the queue.

**The Numbers:**
- Completed: 54 tasks  
- Feature areas: sec-acl-tenant-isolation-20260515, deepsec-run6-security-followup-20260517, migration-squash-2026-05-17, react-doctor-100-followup-sprint


<!-- Generated by dev-tracker publish_to_jekyll.py (AI mode) -->
<!-- accomplished-date: 2026-05-17 -->
<!-- unit-ids: acl-p4-erasure-ledger-tenant-filter,acl-p4-merkle-proof-tenant-filter,acl-p4-suppression-search-tenant-filter,acl-p4-billing-summary-tenant-binding,acl-p4-financial-admin-connection-scope,acl-p4-financial-admin-sync-scope,acl-p4-user-journey-page-props-validation,acl-p4-user-journey-url-client-hardening,acl-p4-feature-flag-adminmiddleware-policy,acl-p4-financial-mutation-route-gates,acl-p4-age-verification-delete-permission,acl-p4-scribe-tryitout-xss,acl-p4-deepsec-high-checkpoint,acl-p4-etl-jobs-route-gates,acl-p4-etl-source-driver-test-gates,acl-p4-financial-view-route-gates,acl-p4-booking-admin-list-permission,acl-p4-codesandbox-ses-local-bootstrap,acl-p4-license-inventory-route-permission,acl-p7-deepsec-run5-checkpoint,acl-p4-license-inventory-api-base-wiring,acl-p6-cicd-group-d-sweep,run6-prod-compose-stack-boundary,run6-k6-remote-import-vendoring,run6-lighthouse-toolchain-pin,run6-dashboard-cache-tenant-scope,run6-scribe-sfdump-regression-guard,migration-squash-2026-05-17-audit-stale-branches,migration-squash-2026-05-17-bootstrap-clean-db,migration-squash-2026-05-17-snapshot-pre-squash,migration-squash-2026-05-17-dump-mysql-schema,migration-squash-2026-05-17-strip-definer,migration-squash-2026-05-17-remove-loadmigrationsfrom,migration-squash-2026-05-17-delete-porto-migrations,migration-squash-2026-05-17-location-guard,migration-squash-2026-05-17-manifest-generator,migration-squash-2026-05-17-equivalence-diff,migration-squash-2026-05-17-resurrection-guard,migration-squash-2026-05-17-makefile-targets,migration-squash-2026-05-17-equivalence-normalization,migration-squash-2026-05-17-sqlite-dump,migration-squash-2026-05-17-fix-mark-squashed-dedup,migration-squash-2026-05-17-verify-migrate-fresh,migration-squash-2026-05-17-runbook,migration-squash-2026-05-17-issues-filed,migration-squash-2026-05-17-commit-and-push,rd100-audit-dead-code-and-react19-buckets,rd100-finish-state-bucket-wave,rd100-finish-hydration-and-intl-wave,rd100-finish-generic-handler-wave,rd100-finish-accessibility-design-wave,rd100-close-root-score-gap,rd100-establish-drift-review-cadence,rd100-archive-sprint-plan -->

<!-- accomplished-unit-ids: acl-p4-age-verification-delete-permission,acl-p4-billing-summary-tenant-binding,acl-p4-booking-admin-list-permission,acl-p4-codesandbox-ses-local-bootstrap,acl-p4-deepsec-high-checkpoint,acl-p4-erasure-ledger-tenant-filter,acl-p4-etl-jobs-route-gates,acl-p4-etl-source-driver-test-gates,acl-p4-feature-flag-adminmiddleware-policy,acl-p4-financial-admin-connection-scope,acl-p4-financial-admin-sync-scope,acl-p4-financial-mutation-route-gates,acl-p4-financial-view-route-gates,acl-p4-license-inventory-api-base-wiring,acl-p4-license-inventory-route-permission,acl-p4-merkle-proof-tenant-filter,acl-p4-scribe-tryitout-xss,acl-p4-suppression-search-tenant-filter,acl-p4-user-journey-page-props-validation,acl-p4-user-journey-url-client-hardening,acl-p6-cicd-group-d-sweep,acl-p7-deepsec-run5-checkpoint,migration-squash-2026-05-17-audit-stale-branches,migration-squash-2026-05-17-bootstrap-clean-db,migration-squash-2026-05-17-commit-and-push,migration-squash-2026-05-17-delete-porto-migrations,migration-squash-2026-05-17-dump-mysql-schema,migration-squash-2026-05-17-equivalence-diff,migration-squash-2026-05-17-equivalence-normalization,migration-squash-2026-05-17-fix-mark-squashed-dedup,migration-squash-2026-05-17-issues-filed,migration-squash-2026-05-17-location-guard,migration-squash-2026-05-17-makefile-targets,migration-squash-2026-05-17-manifest-generator,migration-squash-2026-05-17-remove-loadmigrationsfrom,migration-squash-2026-05-17-resurrection-guard,migration-squash-2026-05-17-runbook,migration-squash-2026-05-17-snapshot-pre-squash,migration-squash-2026-05-17-sqlite-dump,migration-squash-2026-05-17-strip-definer,migration-squash-2026-05-17-verify-migrate-fresh,rd100-archive-sprint-plan,rd100-audit-dead-code-and-react19-buckets,rd100-close-root-score-gap,rd100-establish-drift-review-cadence,rd100-finish-accessibility-design-wave,rd100-finish-generic-handler-wave,rd100-finish-hydration-and-intl-wave,rd100-finish-state-bucket-wave,run6-dashboard-cache-tenant-scope,run6-k6-remote-import-vendoring,run6-lighthouse-toolchain-pin,run6-prod-compose-stack-boundary,run6-scribe-sfdump-regression-guard -->
<!-- SECTION: ACCOMPLISHED END -->
<!-- Generated by dev-tracker build_today_plan.py -->
