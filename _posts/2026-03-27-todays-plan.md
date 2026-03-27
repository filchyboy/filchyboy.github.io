---
layout: post
title: "Daily Plan - 2026-03-27"
date: 2026-03-27
---

# Daily Plan - 2026-03-27

**Generated:** 2026-03-27 14:58 UTC
**Total Time:** 11 hours

## 🎯 Focus Work

### ⚡ production-readiness-master (2 items, 4h) - 9 commits this week, **recently active**, 9% complete

📂 `docs/work/planning/production-readiness-master/`

1. 📋 **PRD-002: TRUSTED_PROXIES Production Configuration** (~1h)
   - Score: 20.4 (recency: +5.0, momentum: +3.0)
   - Why: Highest priority, high business value, urgent, quick win, can start immediately, unblocks 4 downstream items

2. 📋 **PRD-001: Migration Schema Squash** (~3h)
   - Score: 20.4 (recency: +5.0, momentum: +3.0)
   - Why: Highest priority, high business value, urgent, can start immediately, unblocks 4 downstream items

### ⚡ phpstan-pint-file-remediation-harness (1 items, 1h) - 31 commits this week, **recently active**, 1% complete

📂 `docs/work/planning/phpstan-pint-file-remediation-harness/`

1. 📋 **Remediate GetAllUsersTask.php** (~1h)
   - Score: 20.3 (recency: +5.0, momentum: +3.0)
   - Why: High priority, high business value, urgent, quick win, can start immediately

### 📋 api-pagination-guardrails (1 items, 1h) - 5 commits this week, 4 days since last commit

📂 `docs/work/planning/api-pagination-guardrails/`

1. 📋 **Add MAX_PER_PAGE and DEFAULT_PER_PAGE constants to ApiController** (~1h)
   - Score: 19.8 (recency: +3.0, momentum: +2.5)
   - Why: Highest priority, high business value, urgent, quick win, can start immediately, unblocks 1 downstream item

### 📋 thin-vslice-277-dsr-request-management-portal (1 items, 1h) - 5 commits this week, 5 days since last commit

📂 `docs/work/planning/thin-vslice-277-dsr-request-management-portal/`

1. 📋 **TV277: Contract scope baseline** (~1h)
   - Score: 19.3 (recency: +2.5, momentum: +2.5)
   - Why: Highest priority, high business value, urgent, quick win, can start immediately, unblocks 1 downstream item

### 📋 contact-detail-selector-optimization (1 items, 1h) - 5 commits this week, 4 days since last commit

📂 `docs/work/planning/contact-detail-selector-optimization/`

1. 📋 **Create selectContactDetailState composed selector** (~1h)
   - Score: 18.8 (recency: +3.0, momentum: +2.5)
   - Why: Highest priority, high business value, urgent, quick win, can start immediately, unblocks 2 downstream items


## 🎁 Stretch Goals

- Create ImportContactsChunkJob class (csv-import-chunking, ~1h)
- Refactor ImportContactsFromCsvTask to use LazyCollection (csv-import-chunking, ~1h)
- Create DashboardCacheService class (dashboard-metrics-caching, ~1h)

## 📋 Planning Work Needed

### 🔬 Needs Research (2 directories)

- `task-management/` - ticket-details.md missing/empty
- `performance/` - ticket-details.md missing/empty

### 📝 Needs Implementation Plan (12 directories)

- `controller-refactor/` - has research, needs plan
- `dependency-policy/` - has research, needs plan
- `sanctum-security/` - has research, needs plan
- `capacity-planning/` - has research, needs plan
- `cache-strategy/` - has research, needs plan
- ...and 7 more

### 📊 Needs Tracker (1 directories)

- `accessibility-pipeline-enforceable-storybook-gates-component-coverage-kpi-reform/` - has plan, needs tracker.json

## 🚫 Blocked

- **Archive the plan only after the remediation sweep is complete** — blocked by: execute-remediation-sweep
- **Add eager loading to EventAudienceController** — blocked by: eager-enable-query-logging
- **Implement getValidatedPerPage() helper method** — blocked by: pagination-add-constants
- **Add eager loading to MergeSuggestionController** — blocked by: eager-enable-query-logging
- **PRD-006: Sanctum Token Security Configuration** — blocked by: prd-001-migration-squash, prd-002-trusted-proxies
- **TV277: Backend orchestration** — blocked by: tv277-contract-scope-baseline
- **TV277: Data determinism** — blocked by: tv277-backend-orchestration
- **Create lazy wrapper for ControlPlaneTermsRatesPanel** — blocked by: lazy-identify-components
- **Identify top 10 slow query patterns** — blocked by: index-enable-slow-logging
- **Create migration with conditional index creation** — blocked by: index-design-composites
- **Refactor ContactDetail to use composed selector** — blocked by: selector-create-composed
- **Implement Bus::batch() dispatcher for chunked jobs** — blocked by: chunk-lazy-collection, chunk-create-job-class
- **Implement getBillingOverview() with tagged caching** — blocked by: cache-create-service-class
- **Implement getAnalyticsData() with tagged caching** — blocked by: cache-create-service-class
- **Add correlation ID to Log context globally** — blocked by: correlation-create-middleware
- **PRD-005: Disaster Recovery Documentation** — blocked by: prd-001-migration-squash, prd-002-trusted-proxies
- **Add markdownlint comparison section to lint harness compare.py** — blocked by: ratchet-add-markdownlint-utils
- **Add markdownlint regression check to lint harness ratchet.py** — blocked by: ratchet-add-markdownlint-utils
- **TV277: API contract hardening** — blocked by: tv277-data-determinism
- **Create MLAnalyticsController with ~10 ML endpoints** — blocked by: analytics-document-methods
- **Create LoyaltyAnalyticsController with ~10 loyalty endpoints** — blocked by: analytics-document-methods
- **Update 5 high-traffic controllers to use getValidatedPerPage()** — blocked by: pagination-unit-tests
- **Update DashboardController to use DashboardCacheService** — blocked by: cache-billing-overview-method, cache-analytics-method
- **Remove tailwindcss packages and config** — blocked by: tw-p8-remove-tailwind-directives
- **TV277: Frontend integration** — blocked by: tv277-api-contract-hardening
- **TV279: Backend orchestration** — blocked by: tv279-contract-scope-baseline
- **TV279: Data determinism** — blocked by: tv279-backend-orchestration
- **TV280: Backend orchestration** — blocked by: tv280-contract-scope-baseline
- **TV281: Backend orchestration** — blocked by: tv281-contract-scope-baseline
- **TV282: Backend orchestration** — blocked by: tv282-contract-scope-baseline
- **Wrap CrmSyncPanel with React.memo** — blocked by: selector-refactor-component
- **Add eager loading to ChangeSetController** — blocked by: eager-enable-query-logging
- **Add correlation ID to response headers** — blocked by: correlation-create-middleware
- **Update DatabaseQueryListener with correlation ID** — blocked by: correlation-log-context
- **Design composite indexes based on query patterns** — blocked by: index-analyze-patterns
- **Wrap ContactOverview with React.memo** — blocked by: selector-refactor-component
- **Add retry logic with exponential backoff** — blocked by: chunk-create-job-class
- **PRD-007: OpenAPI Specification Migration** — blocked by: prd-001-migration-squash, prd-002-trusted-proxies
- **Add unit tests for selector memoization** — blocked by: selector-create-composed
- **Add markdownlint to lint-harness CI workflow PR comment table** — blocked by: ratchet-add-markdownlint-compare, ratchet-add-markdownlint-ratchet
- **pa11y accessibility audit on all migrated pages** — blocked by: tw-p8-remove-tailwind-packages
- **TV277: Observability instrumentation** — blocked by: tv277-api-contract-hardening
- **TV279: API contract hardening** — blocked by: tv279-data-determinism
- **TV280: Data determinism** — blocked by: tv280-backend-orchestration
- **TV280: API contract hardening** — blocked by: tv280-data-determinism
- **TV281: Data determinism** — blocked by: tv281-backend-orchestration
- **TV281: API contract hardening** — blocked by: tv281-data-determinism
- **TV282: Data determinism** — blocked by: tv282-backend-orchestration
- **TV282: API contract hardening** — blocked by: tv282-data-determinism
- **TV283: Backend orchestration** — blocked by: tv283-contract-scope-baseline
- **Create lazy wrapper for CustomerDetailsPanel** — blocked by: lazy-identify-components
- **Create lazy wrappers for 4+ additional admin components** — blocked by: lazy-wrapper-controlplane
- **Create AdminPanelSkeleton and add Suspense boundaries** — blocked by: lazy-wrapper-controlplane
- **Create CustomerHealthController with ~8 health endpoints** — blocked by: analytics-document-methods
- **Update API routes to use new controllers** — blocked by: analytics-create-ml-controller, analytics-create-loyalty-controller, analytics-create-health-controller, analytics-create-prediction-controller
- **Store batch ID in imports table for tracking** — blocked by: chunk-batch-dispatcher
- **Create batch status API endpoint** — blocked by: chunk-batch-tracking
- **Add model observers for cache invalidation** — blocked by: cache-controller-integration
- **Create job middleware for correlation ID propagation** — blocked by: correlation-log-context
- **Add correlation ID header to frontend API client** — blocked by: correlation-response-header
- **Test migration and verify index usage in staging** — blocked by: index-create-migration
- **Create API routes file for Decision Kernel** — blocked by: dk-p0-controller-intent, dk-p0-controller-record, dk-p0-controller-policy, dk-p0-controller-channel, dk-p0-controller-analytics
- **PRD-004: Large Controller Refactoring** — blocked by: prd-001-migration-squash, prd-002-trusted-proxies
- **PRD-009: Cache Warming Strategy** — blocked by: prd-004-controller-refactor, prd-005-disaster-recovery, prd-006-sanctum-security, prd-007-openapi-migration
- **PRD-011: Dependency Update Policy** — blocked by: prd-004-controller-refactor, prd-005-disaster-recovery, prd-006-sanctum-security, prd-007-openapi-migration
- **Create unit tests for getValidatedPerPage()** — blocked by: pagination-implement-helper
- **Add integration tests for pagination bounds enforcement** — blocked by: pagination-update-high-traffic-controllers
- **Integration tests for large file imports** — blocked by: chunk-batch-dispatcher
- **Create unit tests for DashboardCacheService** — blocked by: cache-invalidation-observers
- **Run markdownlint auto-fix across all docs and commit results** — blocked by: mdlint-enable-autofixable-rules
- **Integration tests for correlation ID propagation** — blocked by: correlation-job-middleware
- **Full BackstopJS visual regression suite** — blocked by: tw-p8-remove-tailwind-packages
- **CSS bundle size audit and optimization** — blocked by: tw-p8-remove-tailwind-packages
- **TV279: Frontend integration** — blocked by: tv279-api-contract-hardening
- **TV280: Frontend integration** — blocked by: tv280-api-contract-hardening
- **TV281: Frontend integration** — blocked by: tv281-api-contract-hardening
- **TV282: Frontend integration** — blocked by: tv282-api-contract-hardening
- **TV283: Data determinism** — blocked by: tv283-backend-orchestration
- **TV283: API contract hardening** — blocked by: tv283-data-determinism
- **TV284: Backend orchestration** — blocked by: tv284-contract-scope-baseline
- **TV284: Data determinism** — blocked by: tv284-backend-orchestration
- **TV284: API contract hardening** — blocked by: tv284-data-determinism
- **Create PredictionController with ~12 prediction endpoints** — blocked by: analytics-document-methods
- **Add eager loading to remaining 15+ controllers** — blocked by: eager-fix-merge-suggestion, eager-fix-event-audience, eager-fix-changeset
- **TV277: Focused tests and accessibility** — blocked by: tv277-frontend-integration, tv277-observability-instrumentation
- **Create StatusBadge component** — blocked by: dk-p2-css-badges-cards, dk-p1-types-enums
- **Create ApprovalCard component** — blocked by: dk-p2-badge-approval
- **Create IntentFilters component** — blocked by: dk-p2-css-base
- **Create ApprovalList with virtualized scrolling** — blocked by: dk-p3-approval-header, dk-p2-card-approval
- **Create ApprovalActions component** — blocked by: dk-p3-approval-list
- **PRD-010: Capacity Planning Guidelines** — blocked by: prd-004-controller-refactor, prd-005-disaster-recovery, prd-006-sanctum-security, prd-007-openapi-migration
- **Update tests and verify 85% coverage** — blocked by: analytics-update-routes
- **Create DecisionIntentController with index, show, store** — blocked by: dk-p0-resource-intent
- **Create DK API CRUD functions** — blocked by: dk-p1-client-endpoints, dk-p1-types-api
- **Create React Query hooks for Decision data** — blocked by: dk-p1-client-functions, dk-p1-types-api
- **Create badge and card CSS styles** — blocked by: dk-p2-css-base
- **Create IntentCard component** — blocked by: dk-p2-badge-status, dk-p2-badge-urgency
- **Create frontmatter migration script with audit/migrate/validate modes** — blocked by: frontmatter-create-schema
- **Python Embedding Microservice Scaffold** — blocked by: COL-7879-1-1-pgvector-docker
- **Database Migration for Embedding Column** — blocked by: COL-7879-1-1-pgvector-docker
- **Embedding Client Service (PHP)** — blocked by: COL-7879-1-5-laravel-config
- **PrecedentSearchService Implementation** — blocked by: COL-7879-1-4-migration-embedding, COL-7879-1-6-embedding-client
- **TV279: Observability instrumentation** — blocked by: tv279-api-contract-hardening
- **TV280: Observability instrumentation** — blocked by: tv280-api-contract-hardening
- **TV281: Observability instrumentation** — blocked by: tv281-api-contract-hardening
- **TV282: Observability instrumentation** — blocked by: tv282-api-contract-hardening
- **TV283: Frontend integration** — blocked by: tv283-api-contract-hardening
- **TV283: Observability instrumentation** — blocked by: tv283-api-contract-hardening
- **TV284: Frontend integration** — blocked by: tv284-api-contract-hardening
- **Update admin dashboard Blade template** — blocked by: frontend-blade-partial
- **Refresh lockfiles after dependency upgrades** — blocked by: vite7-upgrade-root-workspace-dependencies, vite7-upgrade-frontend-workspace-dependencies, vite7-upgrade-laravel-workspace-dependencies, vite7-upgrade-frontend-admin-workspace-dependencies, vite7-upgrade-frontend-remote-workspace-dependencies
- **Align Node versions in GitHub Actions workflows** — blocked by: vite7-pin-node-runtime-contract, vite7-refresh-lockfiles-and-workspace-installs
- **Validate deployment manifest contract** — blocked by: vite7-migrate-laravel-vite-config, vite7-validate-ci-dagger-build-assets
- **Produce implementation handoff summary for next sprint** — blocked by: vite7-update-architecture-and-build-docs, vite7-write-migration-runbook-and-rollback, vite7-capture-quality-gate-artifacts
- **Add bundle size budget check to CI** — blocked by: lazy-chunk-config
- **Update remaining 15+ paginated controllers** — blocked by: pagination-update-high-traffic-controllers
- **Add X-Pagination-Limit-Applied response header** — blocked by: pagination-implement-helper
- **Add EXPLAIN ANALYZE tests to CI** — blocked by: index-test-staging
- **Document index strategy and maintenance** — blocked by: index-ci-explain
- **Add N+1 detection to CI/CD test suite** — blocked by: eager-fix-remaining-controllers
- **TV279: Focused tests and accessibility** — blocked by: tv279-frontend-integration, tv279-observability-instrumentation
- **TV280: Focused tests and accessibility** — blocked by: tv280-frontend-integration, tv280-observability-instrumentation
- **TV281: Focused tests and accessibility** — blocked by: tv281-frontend-integration, tv281-observability-instrumentation
- **TV282: Focused tests and accessibility** — blocked by: tv282-frontend-integration, tv282-observability-instrumentation
- **TV283: Focused tests and accessibility** — blocked by: tv283-frontend-integration, tv283-observability-instrumentation
- **Create API response and pagination types** — blocked by: dk-p1-types-entities
- **Create DK API endpoint definitions** — blocked by: dk-p1-client-base
- **Create ApprovalStatusBadge component** — blocked by: dk-p2-css-badges-cards, dk-p1-types-enums
- **Create PolicyCreateModal with form validation** — blocked by: dk-p4-policy-list, dk-p2-form-policy
- **Create DashboardHeader with period selector** — blocked by: dk-p5-dashboard-shell
- **PRD-008: CSP Hardening - Eliminate unsafe-eval** — blocked by: prd-004-controller-refactor, prd-005-disaster-recovery, prd-006-sanctum-security, prd-007-openapi-migration
- **Create DecisionPolicyController with full CRUD** — blocked by: dk-p0-resource-policy
- **Create KPICards component** — blocked by: dk-p5-dashboard-header
- **Enable manual-fix markdownlint rules (MD029/MD040/MD045/MD055) and fix all violations** — blocked by: mdlint-run-autofix
- **Remove docs/architecture/** from .markdownlintignore and fix violations** — blocked by: mdlint-enable-manual-rules
- **Add max-lines rule to eslint.config.js with legacy exemption array** — blocked by: p1-adr-exemption-policy
- **Run LOC audit and save artifacts/loc-inventory.json** — blocked by: p1-loc-audit-script
- **Phase 4: remove remediated files from legacyMaxLinesExemptFiles** — blocked by: p4-xl-etl-dashboard, p4-xl-kpi-dashboard, p4-xl-cms-widget, p4-xl-codesandbox, p4-xl-roi-analysis, p4-xl-token-organizer, p4-xl-advanced-validator, p4-xl-platform-exporter, p4-lg-keyboard-nav, p4-lg-compat-mapping, p4-lg-admin-components, p4-lg-billing-components, p4-lg-cdp-components, p4-lg-dashboard-components, p4-lg-misc-components, p4-lg-hooks, p4-lg-services, p4-lg-utils, p4-lg-tokens-remaining, p4-lg-misc-source
- **Remove empty legacyMaxLinesExemptFiles array from eslint.config.js** — blocked by: p4-shrink-exemption-list
- **TV277: Quality gates and handoff** — blocked by: tv277-focused-tests-a11y
- **TV279: Quality gates and handoff** — blocked by: tv279-focused-tests-a11y
- **TV280: Quality gates and handoff** — blocked by: tv280-focused-tests-a11y
- **TV281: Quality gates and handoff** — blocked by: tv281-focused-tests-a11y
- **TV282: Quality gates and handoff** — blocked by: tv282-focused-tests-a11y
- **TV283: Quality gates and handoff** — blocked by: tv283-focused-tests-a11y
- **TV284: Observability instrumentation** — blocked by: tv284-api-contract-hardening
- **TV284: Quality gates and handoff** — blocked by: tv284-focused-tests-a11y
- **Add Laravel feature test for dashboard** — blocked by: blade-integration-dashboard-update
- **Guard panel behind feature flag** — blocked by: testing-laravel-feature-test
- **Decide module-federation upgrade path for Vite 7** — blocked by: vite7-verify-upstream-compatibility-matrix
- **Pin Node runtime contract for Vite 7** — blocked by: vite7-verify-upstream-compatibility-matrix
- **Upgrade laravel-app workspace dependencies to Vite 7** — blocked by: vite7-pin-node-runtime-contract
- **Migrate frontend/vite.config.ts for Vite 7 compatibility** — blocked by: vite7-upgrade-frontend-workspace-dependencies
- **Run laravel-app asset build validation after migration** — blocked by: vite7-migrate-laravel-vite-config, vite7-update-build-support-scripts
- **Run module federation runtime smoke validation** — blocked by: vite7-migrate-root-vite-config, vite7-migrate-mfe-vite-configs
- **Validate Dagger and CI build-assets flows** — blocked by: vite7-update-workflow-node-versions, vite7-validate-laravel-assets-gates
- **Publish migration runbook and rollback procedure** — blocked by: vite7-validate-frontend-workspace-gates, vite7-validate-laravel-assets-gates, vite7-validate-federation-runtime-smoke, vite7-validate-ci-dagger-build-assets, vite7-validate-deploy-manifest-contract
- **Capture quality-gate evidence artifacts** — blocked by: vite7-validate-frontend-workspace-gates, vite7-validate-laravel-assets-gates, vite7-validate-federation-runtime-smoke, vite7-validate-ci-dagger-build-assets, vite7-validate-deploy-manifest-contract
- **Authorization and permission tests** — blocked by: dk-p0-routes
- **Accessibility tests for Phase 2 components** — blocked by: dk-p2-form-filters, dk-p2-form-policy
- **Accessibility tests for Phase 3 pages** — blocked by: dk-p3-test-approval, dk-p3-test-detail
- **Accessibility tests for Phase 4 pages** — blocked by: dk-p4-test-policy, dk-p4-test-prefs
- **Accessibility tests for Phase 5 pages** — blocked by: dk-p5-test-dashboard, dk-p5-test-analytics, dk-p5-test-history
- **Configure chunk naming for admin modules** — blocked by: lazy-wrapper-additional
- **Update API documentation with deprecation notices** — blocked by: analytics-update-routes
- **Update API documentation with pagination limits** — blocked by: pagination-integration-tests
- **Create performance benchmark documentation** — blocked by: selector-memo-contactoverview, selector-memo-crmsyncpanel
- **Update frontend to poll batch status** — blocked by: chunk-status-endpoint
- **Add cache metrics to monitoring dashboard** — blocked by: cache-unit-tests
- **Add correlation ID search to log dashboard** — blocked by: correlation-integration-tests
- **TV284: Focused tests and accessibility** — blocked by: tv284-frontend-integration, tv284-observability-instrumentation
- **Create DecisionRecordController with index by intent, show** — blocked by: dk-p0-resource-record
- **Create ModeBadge component** — blocked by: dk-p2-css-badges-cards, dk-p1-types-enums
- **Create ApprovalQueueHeader component** — blocked by: dk-p3-approval-shell
- **Implement polling-based real-time updates** — blocked by: dk-p3-approval-list, dk-p1-hooks
- **Create IntentHeader with status, actions, breadcrumb** — blocked by: dk-p3-detail-shell, dk-p2-badge-status
- **Create IntentSummary component** — blocked by: dk-p3-detail-header
- **Create PolicyList component with filtering** — blocked by: dk-p4-policy-shell, dk-p2-card-policy
- **Create DecisionVolumeChart with Recharts BarChart** — blocked by: dk-p5-dashboard-kpis
- **Remove docs/security/** and docs/api/** from .markdownlintignore and fix violations** — blocked by: mdlint-remove-architecture-ignore
- **Remove docs/operations/** from .markdownlintignore and fix violations** — blocked by: mdlint-remove-security-api-ignore
- **Update documentation templates and metadata scripts for YAML frontmatter** — blocked by: frontmatter-create-schema
- **Migrate docs/architecture/ and docs/api/ files to YAML frontmatter** — blocked by: frontmatter-create-migration-script
- **Migrate docs/user-guides/ and docs/development/ files to YAML frontmatter** — blocked by: frontmatter-create-migration-script
- **Enable link markdownlint rules and add link validation to CI** — blocked by: links-normalize-all
- **Create performance benchmark tests** — blocked by: eager-fix-remaining-controllers
- **Phase 2: remove remediated files from legacyMaxLinesExemptFiles** — blocked by: p2-qw-admin-components, p2-qw-core-components-a, p2-qw-core-components-b, p2-qw-billing-components, p2-qw-cdp-components, p2-qw-compliance-security, p2-qw-dashboard-design-system, p2-qw-misc-components, p2-qw-hooks-hocs, p2-qw-services, p2-qw-sdk-types-misc
- **Phase 3: remove remediated files from legacyMaxLinesExemptFiles** — blocked by: p3-med-admin-a, p3-med-admin-b, p3-med-core-a, p3-med-core-b, p3-med-cdp, p3-med-dashboard, p3-med-billing, p3-med-misc-components, p3-med-hooks, p3-med-services, p3-med-tokens, p3-med-utils-misc
- **Large: ETLDashboard.tsx (1,160 LOC)** — blocked by: p3-shrink-exemption-list
- **Large: KpiDashboard (1,043 LOC) + EtlPerformanceCharts (827 LOC)** — blocked by: p3-shrink-exemption-list
- **Large: CMSContentWidget.tsx (1,033 LOC)** — blocked by: p3-shrink-exemption-list
- **Resolve billing account and build HealthProbeContext::forBillingAccountId in request lifecycle** — blocked by: tenant-probes-route-design
- **Docker Compose Integration for Embedding Service** — blocked by: COL-7879-1-2-python-microservice
- **SearchPrecedentsAction** — blocked by: COL-7879-2-1-precedent-service
- **Add dedicated Vite entry point for admin dashboard** — blocked by: frontend-build-strategy-decision
- **Update coverage thresholds to 30% (Month 1 milestone)** — blocked by: a11y-core-components-batch-1
- **Fix hit-area rule false positives with CSS custom properties** — blocked by: a11y-core-components-batch-1
- **Migrate laravel-app/vite.config.js for Vite 7 compatibility** — blocked by: vite7-upgrade-laravel-workspace-dependencies
- **Run frontend workspace quality gates after migration** — blocked by: vite7-migrate-frontend-vite-config, vite7-update-build-support-scripts
- **Feature tests for end-to-end API flows** — blocked by: dk-p0-routes
- **Integration tests for Approval Queue page** — blocked by: dk-p3-approval-polling
- **Create PolicyCard component** — blocked by: dk-p2-css-badges-cards
- **Create PolicyEditor component** — blocked by: dk-p2-css-base
- **Create ApprovalDetailModal for quick review** — blocked by: dk-p3-approval-actions
- **Create ApprovalTimeline component** — blocked by: dk-p3-detail-summary
- **Create PolicyEditModal with version comparison** — blocked by: dk-p4-policy-create
- **Quick-win: CDP components (4 files, 226-300 LOC)** — blocked by: p1-eslint-max-lines-rule
- **Create decisionSlice Redux state** — blocked by: dk-p1-types-entities
- **Create async thunks for Decision API calls** — blocked by: dk-p1-redux-slice, dk-p1-client-functions
- **Migrate all remaining docs to YAML frontmatter and enable MD041** — blocked by: frontmatter-migrate-architecture-api, frontmatter-migrate-userguides-dev
- **Run link normalization across all docs and commit results** — blocked by: links-create-normalize-script, links-run-audit-repair
- **Generate README.md stubs for 30+ directories missing them** — blocked by: readme-create-stub-script
- **Add frontmatter-validate and todo-audit to docs-governance-check Makefile target** — blocked by: frontmatter-create-migration-script, todo-audit-consolidate
- **Large: CodeSandboxService.ts (1,095 LOC)** — blocked by: p3-shrink-exemption-list
- **Large: ROIAnalysis.tsx (983 LOC)** — blocked by: p3-shrink-exemption-list
- **Implement tenant-aware checks in probes that need more than platform DB ping** — blocked by: tenant-probes-context-middleware
- **Tests, PHPStan, and ops docs for per-tenant feature health** — blocked by: tenant-probes-slice-logic
- **Phase 2: Backend audit logging** — blocked by: mfa-audit-logs-phase-1-database-and-model
- **Laravel Configuration for Embedding Service** — blocked by: COL-7879-1-2-python-microservice
- **Batch Embedding Generation Job** — blocked by: COL-7879-1-4-migration-embedding, COL-7879-1-6-embedding-client
- **Similarity Search with Filtering** — blocked by: COL-7879-2-1-precedent-service
- **Incremental Embedding Generation** — blocked by: COL-7879-1-6-embedding-client, COL-7879-2-1-precedent-service
- **Service Provider Updates** — blocked by: COL-7879-2-1-precedent-service, COL-7879-2-3-incremental-embedding
- **Unit Tests for PrecedentSearchService** — blocked by: COL-7879-2-1-precedent-service, COL-7879-2-2-filtering
- **PrecedentSearchController** — blocked by: COL-7879-3-1-search-action, COL-7879-3-2-form-request
- **Integration Tests for API** — blocked by: COL-7879-3-3-controller, COL-7879-3-4-routes
- **CI/CD Pipeline Updates** — blocked by: COL-7879-1-1-pgvector-docker, COL-7879-1-2-python-microservice, COL-7879-1-3-docker-integration
- **Implement Blade partial for resilience analytics panel** — blocked by: frontend-build-strategy-decision
- **Add accessibility tests for 30 core components (Button, Input, Select, etc.)** — blocked by: a11y-storybook-hooks-migration, a11y-install-addon-links, a11y-fix-jest-haste-collisions
- **Create reusable accessibility test templates** — blocked by: a11y-core-components-batch-1
- **Upgrade root workspace Vite toolchain to Vite 7** — blocked by: vite7-decide-federation-path, vite7-pin-node-runtime-contract
- **Upgrade frontend workspace dependencies to Vite 7** — blocked by: vite7-pin-node-runtime-contract
- **Upgrade frontend-admin workspace dependencies to Vite 7** — blocked by: vite7-decide-federation-path, vite7-pin-node-runtime-contract
- **Migrate root vite.config.ts for Vite 7 compatibility** — blocked by: vite7-upgrade-root-workspace-dependencies, vite7-upgrade-frontend-admin-workspace-dependencies, vite7-upgrade-frontend-remote-workspace-dependencies
- **Update build/support scripts that invoke Vite** — blocked by: vite7-refresh-lockfiles-and-workspace-installs, vite7-migrate-root-vite-config, vite7-migrate-frontend-vite-config, vite7-migrate-laravel-vite-config, vite7-migrate-mfe-vite-configs
- **Run make css-modules-harness-snapshot and verify baseline** — blocked by: css-verify-reports
- **Unit tests for DecisionIntent API endpoints** — blocked by: dk-p0-controller-intent
- **Unit tests for DecisionPolicy CRUD** — blocked by: dk-p0-controller-policy
- **Unit tests for badge components** — blocked by: dk-p2-badge-status, dk-p2-badge-mode, dk-p2-badge-approval, dk-p2-badge-urgency
- **Integration tests for Intent Detail page** — blocked by: dk-p3-detail-payload
- **Add OpenAPI documentation annotations** — blocked by: dk-p0-routes
- **Create Redux selectors for computed state** — blocked by: dk-p1-redux-slice
- **Create UrgencyIndicator component** — blocked by: dk-p2-css-badges-cards
- **Create Storybook stories for Phase 2 components** — blocked by: dk-p2-test-a11y
- **Create ExecutionTimeline component** — blocked by: dk-p3-detail-approval-timeline, dk-p2-card-step
- **Create RulesJsonEditor with syntax highlighting** — blocked by: dk-p4-policy-edit
- **Create PolicyActivationToggle with confirmation** — blocked by: dk-p4-policy-json-editor
- **Create ChannelProfileList component** — blocked by: dk-p4-prefs-shell, dk-p2-card-channel
- **Create ChannelPreferencesEditor component** — blocked by: dk-p4-prefs-list, dk-p2-form-channel
- **Create QuickActionsPanel component** — blocked by: dk-p5-dashboard-recent
- **Create DecisionTrendsChart with Recharts LineChart** — blocked by: dk-p5-analytics-shell
- **Create ExportControls component** — blocked by: dk-p5-chart-policy
- **Create DecisionHistoryTable with sorting, pagination** — blocked by: dk-p5-history-shell
- **Create AuditTrailExport component** — blocked by: dk-p5-history-filters
- **Quick-win: core components batch B (8 files, 226-300 LOC)** — blocked by: p1-eslint-max-lines-rule
- **Quick-win: billing components (7 files, 226-300 LOC)** — blocked by: p1-eslint-max-lines-rule
- **Quick-win: dashboard + design-system components (5 files, 226-300 LOC)** — blocked by: p1-eslint-max-lines-rule
- **Medium: admin components batch B (8 files, 301-500 LOC)** — blocked by: p2-shrink-exemption-list
- **Medium: core components batch A (7 files, 301-500 LOC)** — blocked by: p2-shrink-exemption-list
- **Medium: core components batch B (7 files, 301-500 LOC)** — blocked by: p2-shrink-exemption-list
- **Medium: CDP components (9 files, 301-500 LOC)** — blocked by: p2-shrink-exemption-list
- **Create DecisionAnalyticsController for overview, trends** — blocked by: dk-p0-resource-intent, dk-p0-resource-record
- **Create README stub generation script for directories missing READMEs** — blocked by: frontmatter-create-schema
- **Add markdownlint/links/frontmatter rows to lint-harness PR comment** — blocked by: ratchet-update-ci-workflow, links-enable-mdlint-rules-ci
- **Quick-win: admin components (15 files, 226-300 LOC)** — blocked by: p1-eslint-max-lines-rule
- **Quick-win: core components batch A (8 files, 226-300 LOC)** — blocked by: p1-eslint-max-lines-rule
- **Quick-win: hooks and HOCs (3 files, 226-300 LOC)** — blocked by: p1-eslint-max-lines-rule
- **Quick-win: services (3 files, 226-300 LOC)** — blocked by: p1-eslint-max-lines-rule
- **Medium: admin components batch A (9 files, 301-500 LOC)** — blocked by: p2-shrink-exemption-list
- **Medium: dashboard components (8 files, 301-500 LOC)** — blocked by: p2-shrink-exemption-list
- **Large: token-organizer.ts (1,559 LOC)** — blocked by: p3-shrink-exemption-list
- **Large: advanced-validator.ts (1,366 LOC)** — blocked by: p3-shrink-exemption-list
- **Large: platform-exporter (1,150 LOC) + json-exporter (815 LOC)** — blocked by: p3-shrink-exemption-list
- **Large: keyboardNavigation.ts (935 LOC)** — blocked by: p3-shrink-exemption-list
- **Large: admin components (7 files, 501+ LOC)** — blocked by: p3-shrink-exemption-list
- **Large: billing components (7 files, 501+ LOC)** — blocked by: p3-shrink-exemption-list
- **Verify CI blocks new files exceeding 225 LOC** — blocked by: p6-remove-legacy-array
- **Phase 3: API enhancement** — blocked by: mfa-audit-logs-phase-2-backend-audit-logging
- **SearchPrecedentsRequest Form Request** — blocked by: COL-7879-3-1-search-action
- **API Routes for Precedent Search** — blocked by: COL-7879-3-3-controller
- **Update build pipeline for new entry point** — blocked by: frontend-vite-entry-point
- **Run token validation scripts** — blocked by: css-token-scss-audit
- **Monitor admin dashboard metrics post-deploy** — blocked by: rollout-feature-flag
- **Prepare release notes** — blocked by: rollout-feature-flag
- **Update coverage thresholds to 50% (Month 2 milestone)** — blocked by: a11y-dashboard-components-batch-1
- **Add accessibility tests for 25 dashboard KPI & chart components** — blocked by: a11y-core-components-batch-1
- **Implement enhanced color contrast custom axe rule** — blocked by: a11y-core-components-batch-1
- **Implement focus indicator visibility custom axe rule** — blocked by: a11y-color-contrast-rule
- **Create CLI tool for accessibility test scaffolding** — blocked by: a11y-test-templates
- **Align Redux ecosystem dependencies** — blocked by: rtk-upgrade-inventory
- **Build validation loop** — blocked by: rtk-upgrade-extrareducers, rtk-upgrade-action-types, rtk-upgrade-selectors, rtk-upgrade-thunks, rtk-upgrade-immer, rtk-upgrade-component-refs, rtk-upgrade-component-props, rtk-upgrade-css-properties, rtk-upgrade-services, rtk-upgrade-storybook-stories, rtk-upgrade-token-validator
- **Test suite validation** — blocked by: rtk-upgrade-build-validation
- **Lock dependencies and document** — blocked by: rtk-upgrade-quality-gates
- **Migrate frontend-admin and frontend-remote-example Vite configs** — blocked by: vite7-upgrade-frontend-admin-workspace-dependencies, vite7-upgrade-frontend-remote-workspace-dependencies
- **Update architecture/build documentation for Vite 7** — blocked by: vite7-migrate-root-vite-config, vite7-migrate-frontend-vite-config, vite7-migrate-laravel-vite-config, vite7-migrate-mfe-vite-configs
- **API client unit tests with MSW mocking** — blocked by: dk-p1-client-functions
- **Redux slice unit tests** — blocked by: dk-p1-redux-thunks
- **React Query hooks tests** — blocked by: dk-p1-hooks
- **Unit tests for card components** — blocked by: dk-p2-card-intent, dk-p2-card-approval, dk-p2-card-policy
- **Integration tests for Policy Management page** — blocked by: dk-p4-policy-activation
- **Integration tests for Dashboard page** — blocked by: dk-p5-dashboard-quick
- **Resource transformation tests** — blocked by: dk-p0-resource-intent, dk-p0-resource-record, dk-p0-resource-policy
- **Create ExecutionStepCard component** — blocked by: dk-p2-css-badges-cards
- **Create ChannelPreferencesForm component** — blocked by: dk-p2-css-base
- **Create QuietHoursEditor component** — blocked by: dk-p2-css-base
- **Create PayloadViewer component** — blocked by: dk-p3-detail-exec-timeline
- **Create PolicyVersionHistory component** — blocked by: dk-p4-policy-list
- **Create QuietHoursScheduler with visual time picker** — blocked by: dk-p4-prefs-editor, dk-p2-form-quiethours
- **Create ContentClassificationManager component** — blocked by: dk-p4-prefs-quiethours
- **Create StatusDistributionChart with Recharts PieChart** — blocked by: dk-p5-chart-volume
- **Create RecentDecisionsList component** — blocked by: dk-p5-chart-status
- **Create ModeDistributionChart showing human vs agent** — blocked by: dk-p5-chart-trends
- **Create ApproverPerformanceTable component** — blocked by: dk-p5-chart-mode
- **Create PolicyUsageChart showing policy effectiveness** — blocked by: dk-p5-analytics-approvers
- **Create HistoryFilters with advanced filtering** — blocked by: dk-p5-history-table
- **Quick-win: compliance + security components (7 files, 226-300 LOC)** — blocked by: p1-eslint-max-lines-rule
- **Medium: billing components (5 files, 301-500 LOC)** — blocked by: p2-shrink-exemption-list
- **Test: Transform accomplished.json to markdown** — blocked by: reform-bip-create-tests
- **Test: Group units by feature_set** — blocked by: reform-bip-create-tests
- **Test: Generate correct post filename from date** — blocked by: reform-bip-create-tests
- **Update docs/build_in_public/README.md** — blocked by: reform-bip-update-user-guide
- **Create ChannelProfileCard component** — blocked by: dk-p2-css-badges-cards
- **Run filename fixes across docs and update internal references** — blocked by: naming-implement-fix-mode
- **Create stale documentation detection script** — blocked by: frontmatter-migrate-remaining
- **Flag and archive stale documentation content** — blocked by: stale-create-detector
- **Medium: hooks (7 files, 301-500 LOC)** — blocked by: p2-shrink-exemption-list
- **Medium: services (8 files, 301-500 LOC)** — blocked by: p2-shrink-exemption-list
- **Medium: token system files (8 files, 301-500 LOC)** — blocked by: p2-shrink-exemption-list
- **Large: CDP components (3 files, 501+ LOC)** — blocked by: p3-shrink-exemption-list
- **Large: dashboard components (4 files, 501+ LOC)** — blocked by: p3-shrink-exemption-list
- **Large: hooks (4 files, 501+ LOC)** — blocked by: p3-shrink-exemption-list
- **Large: services (9 files, 501+ LOC)** — blocked by: p3-shrink-exemption-list
- **Large: utils (5 files, 501+ LOC)** — blocked by: p3-shrink-exemption-list
- **Large: token system files (12 files, 501+ LOC)** — blocked by: p3-shrink-exemption-list
- **Add LOC domain to lint harness ratchet system** — blocked by: p6-remove-legacy-array
- **Artisan Command for Batch Embedding** — blocked by: COL-7879-1-7-batch-job
- **Unit Tests for Embedding Client** — blocked by: COL-7879-1-6-embedding-client
- **Decision Workflow Integration** — blocked by: COL-7879-3-1-search-action
- **Performance Testing Setup** — blocked by: COL-7879-2-1-precedent-service
- **Provide non-JS fallback skeleton** — blocked by: frontend-blade-partial
- **Implement keyboard trap detection custom axe rule** — blocked by: a11y-focus-indicator-rule
- **Convert extraReducers to builder callbacks** — blocked by: rtk-upgrade-dependencies
- **Fix custom action types** — blocked by: rtk-upgrade-dependencies
- **Fix thunk and hook typing** — blocked by: rtk-upgrade-dependencies
- **Fix service layer typing** — blocked by: rtk-upgrade-dependencies
- **Run quality gates** — blocked by: rtk-upgrade-test-validation
- **Code review and approval** — blocked by: rtk-upgrade-documentation
- **Run make a11y-harness-status and verify dashboard renders** — blocked by: a11y-verify-snapshot
- **Run make a11y-harness-compare and verify zero-delta** — blocked by: a11y-verify-snapshot
- **Unit tests for Analytics endpoints** — blocked by: dk-p0-controller-analytics
- **Integration tests for User Preferences page** — blocked by: dk-p4-prefs-classification
- **Integration tests for Analytics page** — blocked by: dk-p5-analytics-export
- **Integration tests for History page** — blocked by: dk-p5-history-export
- **Test: Handle empty accomplished report** — blocked by: reform-bip-create-tests
- **Create documentation quality gates standards guide** — blocked by: ci-expand-governance-check, ci-expand-pr-comment
- **Quick-win: remaining component directories (26 files, 226-300 LOC)** — blocked by: p1-eslint-max-lines-rule
- **Medium: remaining component directories (31 files, 301-500 LOC)** — blocked by: p2-shrink-exemption-list
- **Update agents/50_frontend.md with max-lines rule documentation** — blocked by: p6-remove-legacy-array
- **Add Scribe/OpenAPI entries for resilience analytics endpoints** — blocked by: backend-route-provider-registration
- **Add JS/Playwright coverage for interactions** — blocked by: frontend-blade-partial
- **Update operations and admin dashboard docs** — blocked by: blade-integration-dashboard-update
- **Update coverage thresholds to 70% (Month 3 milestone)** — blocked by: a11y-admin-components-batch-2
- **Add accessibility tests for 25 dashboard data table & filter components** — blocked by: a11y-dashboard-components-batch-1
- **Fix selector memoization and typing** — blocked by: rtk-upgrade-dependencies
- **Fix Immer and event map typings** — blocked by: rtk-upgrade-dependencies
- **Fix component ref typing issues** — blocked by: rtk-upgrade-dependencies
- **Fix component prop type mismatches** — blocked by: rtk-upgrade-dependencies
- **Fix custom CSS property typing** — blocked by: rtk-upgrade-dependencies
- **Fix Storybook server startup** — blocked by: rtk-upgrade-storybook-stories
- **Update documentation** — blocked by: rtk-upgrade-dependency-lockdown
- **Upgrade frontend-remote-example workspace dependencies to Vite 7** — blocked by: vite7-decide-federation-path, vite7-pin-node-runtime-contract
- **Large: compatibility-mapping.ts (904 LOC)** — blocked by: p3-shrink-exemption-list
- **Test: Handle report with no completed units** — blocked by: reform-bip-create-tests
- **Delete stale SESSION-SUMMARY-2025-12-10.md from repo root** — blocked by: p1-adr-exemption-policy
- **Quick-win: sdk, types, store, design, utils, tokens, examples, web-components (10 files, 226-300 LOC)** — blocked by: p1-eslint-max-lines-rule
- **Medium: utils, sdk, tests, types, store, web-components, misc (14 files, 301-500 LOC)** — blocked by: p2-shrink-exemption-list
- **Large: remaining component directories (21 files, 501+ LOC)** — blocked by: p3-shrink-exemption-list
- **Phase 4: Frontend integration** — blocked by: mfa-audit-logs-phase-3-api-enhancement
- **Cursor-Based Pagination** — blocked by: COL-7879-3-3-controller
- **HNSW Index Optimization** — blocked by: COL-7879-1-4-migration-embedding
- **Query Plan Analysis** — blocked by: COL-7879-4-2-index-optimization
- **API Documentation** — blocked by: COL-7879-3-3-controller
- **Ensure localization strings exist** — blocked by: blade-integration-dashboard-update
- **Update coverage thresholds to 90% (Final production target)** — blocked by: a11y-utility-components-final-batch
- **Add accessibility tests for 50 admin components (user management, settings)** — blocked by: a11y-dashboard-components-batch-2
- **Implement ARIA live region validation custom axe rule** — blocked by: a11y-keyboard-trap-rule
- **Update accessibility testing guide documentation** — blocked by: a11y-test-generation-cli
- **Add Storybook story typing** — blocked by: rtk-upgrade-dependencies
- **Fix token validator and Ajv typing** — blocked by: rtk-upgrade-dependencies
- **Add function to merge new content into existing post** — blocked by: reform-bip-locate-existing-post
- **Add deprecation header to publish-to-jekyll-blog.sh** — blocked by: reform-bip-update-user-guide
- **Add deprecation header to generate-build-in-public-summary.sh** — blocked by: reform-bip-update-user-guide
- **Add deprecation header to publish-build-in-public.sh** — blocked by: reform-bip-update-user-guide
- **Large: remaining source files (5 files, 501+ LOC)** — blocked by: p3-shrink-exemption-list
- **Phase 5: Testing and documentation** — blocked by: mfa-audit-logs-phase-4-frontend-integration
- **Scaling Guide Documentation** — blocked by: COL-7879-4-1-performance-tests, COL-7879-4-2-index-optimization, COL-7879-4-3-query-analysis
- **Load Testing** — blocked by: COL-7879-3-3-controller, COL-7879-4-1-performance-tests
- **Document new design tokens** — blocked by: css-token-validation
- **Create ADR for accessibility testing standards** — blocked by: a11y-threshold-90-percent
- **Update accessibility compliance report generation** — blocked by: a11y-threshold-90-percent
- **Phase 6: Admin reporting interface** — blocked by: mfa-audit-logs-phase-5-testing-and-docs
- **Add deprecation header to extract-commit-info.py** — blocked by: reform-bip-update-user-guide
- **Add deprecation header to extract-tweets.py** — blocked by: reform-bip-update-user-guide
- **Add accessibility tests for 50 admin components (config, monitoring, access)** — blocked by: a11y-admin-components-batch-1
- **Add accessibility tests for 87 utility & helper components (template-based)** — blocked by: a11y-test-generation-cli, a11y-admin-components-batch-2
- **Add accessibility tests for final 88 utility components** — blocked by: a11y-utility-components-batch-1

## 📌 Notes

- 406 item(s) blocked - check dependencies
- Total estimated time: 8 hours
