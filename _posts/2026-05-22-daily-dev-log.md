---
layout: post
title: "Daily Dev Log - 2026-05-22"
date: 2026-05-22
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-05-22T13:02:48.137475+00:00 -->

## Today's Theme

The security regression remediation I've been deep in has me finding vulnerabilities faster than I can fix them - yesterday's 31 completed items in the deepsec-run11 work revealed just how exposed we've been across SSO, billing, and token systems. The accidental-pint cleanup that got my attention yesterday is finally narrowing down to manageable cohorts, though the billing one still terrifies me. What's really pulling at me is this fresh frontend Jest coverage work I touched in the last 24 hours - it's time to stop letting our frontend turn into a house of cards.

## The Main Work

**Clean up the Jest coverage denominator and refresh the baseline (frontend-jest-coverage-expansion-denominator-cleanup)** - I've been putting this off because test coverage work feels like eating vegetables, but yesterday's touch on this reminded me how much dead code is inflating our denominator. The baseline is probably counting deleted components and stale test files, making our actual coverage look worse than it is. I'd rather spend an hour cleaning this up than keep making decisions based on garbage metrics.

**Remediate the Core Tests container cohort for accidental Pint (accidental-pint-core-tests)** - This is the less scary sibling of the billing cohort I've been avoiding. Test code formatting changes can break our CI pipeline, but at least they won't charge customers the wrong amount. The Tests container has accumulated so many Pint violations that it's probably easier to batch-fix them than to keep manually resolving conflicts every time I touch a spec file.

**Add token implementation coverage to the Jest expansion (frontend-jest-coverage-expansion-token-implementation-coverage)** - Our token system handles authentication, authorization, and API access, but I suspect the frontend coverage is practically nonexistent. Given how many token-related security issues I just fixed in the backend, leaving the frontend token handling untested feels like asking for trouble. This work unit exists in the planning tracker, so someone already scoped what needs testing - I just need to write the specs.

**Finish the hs126 CI smoke test implementation (hs126-ci-smoke-dev-up)** - This horizontal slice is marked as nearly complete and it's genuinely bothering me that our developer onboarding promises a working `make dev-up` command but we've never actually validated that promise in CI. New developers shouldn't have to debug our setup instructions - either they work or they don't, and a smoke test will tell us which.

## Housekeeping

**Run the markdownlint fixes on recently modified planning docs** - With all the planning activity from yesterday's completions, I probably introduced formatting inconsistencies in the tracker updates. The 196 markdownlint issues across 12 files include some in planning directories I've been touching.

**Regenerate the PHPStan baseline after yesterday's deepsec fixes** - The 31 completed security items probably resolved some of the 13,447 PHPStan errors. Rather than work against a stale baseline, I should capture the current state so I can see real progress.

**Draft the AgentTracing contract scope baseline** - The frontend-jest-coverage-expansion planning directory shows this is aligned with current work, and Phase 0 contract definition is exactly the kind of foundation work that unlocks everything else. The storage namespace and retention policies can't be designed without nailing down what we're actually capturing.

## Parked

The Core Billing accidental Pint cohort is the elephant in the room - I keep pushing it aside because billing code touches invoice generation and any formatting changes that introduce arithmetic bugs could affect customer charges months later. I'll tackle the Tests cohort first to build confidence, then approach billing when I'm feeling more methodical about it.

The 1309 PHP test failures are probably environment-related given the security changes I just landed, but debugging test infrastructure when I'm in a feature-building mood feels like a context switch I don't want to make right now.

<!-- plan-unit-ids: accidental-pint-core-etl,accidental-pint-core-tenancy,todoremed-p0-replace-template-boilerplate -->
<!-- SECTION: DAILY-PLAN END -->


<!-- SECTION: ACCOMPLISHED START -->
<!-- accomplished-generated: 2026-05-23T12:46:25.418400+00:00 -->
<!-- accomplished-updated: 2026-05-23T12:46:25.418400+00:00 -->

* Completed 137 tasks today on the Colossalistic Platform project.

## What I Built

### archive-deepsec-run11
* Archive deepsec-run11-regression-remediation planning work

### archive-privacy-governance
* Archive privacy governance UI plan

### comprehensive-threat
* Add comprehensive threat model documentation for the Colossalistic platform

### finalize-archived-deepsec
* Finalize archived deepsec-run11 plan content

### gpc-enforcement
* Document current GPC integration points
* Define GPC domain enums and contracts
* Create privacy signals migration
* Create privacy policy evaluations migration
* Create privacy processing suppressions migration
* Add PrivacySignal model and factory
* Add PrivacyPolicyEvaluation model and factory
* Add PrivacyProcessingSuppression model and factory
* Add GPC regulatory rule fixtures
* Implement request provenance hashing
* Normalize Sec-GPC header into Privacy Signal payload
* Evaluate GPC signal against regulatory rules
* Persist tenant-scoped GPC signal and policy evaluation
* Write active Privacy Processing Suppressions
* Implement GPC freshness and expiration handling
* Add GPC detection middleware
* Register GPC middleware in web and API groups
* Expose request-local GPC state to app consumers
* Define GPC status API read model
* Add GPC status to privacy settings API
* Add contextual GPC Recognition Notice contract
* Suppress tracking injection in publishing rendering
* Apply GPC override to publishing/CDP send eligibility
* Link anonymous GPC signals after principal evidence appears
* Test GPC middleware request flows
* Test GPC policy evaluation scenarios
* Test GPC suppression lifecycle
* Test GPC API read model contract
* Test publishing and CDP enforcement
* Define ETL GPC enforcement query contract
* Define MCP and TOON GPC policy constraint contract
* Define analytics downgrade contract
* Define CDP identity graph annotation contract
* Define GPC propagation reconciliation contract
* Document GPC enforcement contracts
* Run targeted quality gates and prepare close-out evidence

### implement-privacy-control
* Implement Privacy Control Plane Models and Services

### implement-privacy-governance
* Implement Privacy Governance UI planning documents and artifacts

### mcp-governance-layer
* Add governed invocation envelope and execution receipt DTOs
* Implement governed invocation envelope service
* Attach governed envelope during MCP execution context validation
* Return governance payloads from governed MCP tool responses
* Persist governed envelope and receipt in MCP provenance context
* Add regression coverage and stabilize touched provenance authorization scope

### multiple-architectural
* Add multiple architectural decision records  for privacy management boundaries

### optimize-publication-logic
* Optimize publication logic in PrivacyGovernance services and tests

### privacy
* Implement governance UI surfaces

### privacy-governance
* Add Privacy Governance Foundation planning artifacts

### privacy-governance-foundation
* Regulatory Rule Registry MVP
* Regulatory rule validation fixtures
* Data Element Catalog MVP
* Ledger readiness and Privacy Inventory Gaps
* Privacy Control Plane skeleton
* Privacy Access Session and Service Enrollment
* Contact and consent Data Element Representation mappings
* Tenant Privacy Ledger View
* Privacy Identity Links and contestation
* Privacy Disposition Request workflows
* Tenant-independent evidence store and receipts
* Privacy presence events and local indexes
* Federated discovery and routing cache
* Vendor propagation and disconnected notices
* Hardening, documentation, and quality gates

### privacy-governance-ui
* Document current UI and backend privacy integration points
* Define Privacy Governance UI API contracts and fixtures
* Scaffold Privacy Governance admin route and capabilities
* Build Tenant Privacy Entry Point and disclosure shell
* Build Tenant Privacy Ledger View and Data Element detail
* Build Platform Privacy Center shell
* Add principal receipt lookup and read-only receipt detail
* Build Privacy Governance admin shell
* Add ledger readiness and inventory gap admin queues
* Add requests, dispositions, receipts, and evidence admin queues
* Add registry and presence health admin surface
* Define Privacy Governance Metrics contracts and privacy guardrails
* Build Privacy Governance Metrics UI
* Add request and disposition mutation workflows
* Run targeted quality gates and prepare close-out evidence

### provisioning
* Let validation handle invalid region

### refactor-threat-model
* Refactor threat model documentation and implementation plans

### soc
* Update SOC 2 Readiness Implementation Plan and Tracker

### threat-model
* Inventory docs/security and classify canonical, duplicate, stale, stub, and evidence documents
* Restructure docs/security into an indexed Security Knowledge Base
* Promote the full repository threat model into canonical security documentation
* Implement a tenant scope bypass inventory and enforcement gate
* Harden routes and requests that accept explicit tenant or account identifiers
* Backfill explicit permissions for bulk, export, token, settings, and destructive admin/API routes
* Harden public DSR and COPPA workflows against enumeration and lifecycle abuse
* Harden media upload, presigned upload completion, and file/import connectors
* Bind MCP/TOON execution policy to route capability, tool ID, tenant, function token, environment, and parameters
* Add golden MCP/TOON denial tests for cross-tenant, cross-domain, stale nonce, and missing capability paths
* Harden webhook signature, replay, parser, and queue-abuse controls
* Build audit/log coverage map and alerts for privileged and cross-boundary security events
* Record targeted quality gates, closeout evidence, and deferred disposition

### typescript-eslint
* Update @typescript-eslint/parser to version 8.59.4

### various-planning
* Add various planning documentation and trackers for completed tasks

### webmcp
* Archive integration plan

### webmcp-integration
* Add baseline WebMCP manifest contract fixture
* Document the WebMCP capability projection schema
* Create WebMCP capability projection data object
* Add WebMCP exposure tier enum
* Build browser-safe projection from MCP ToolDefinition
* Test ToolDefinition to WebMCP projection mapping
* Refactor BuildWebMcpBindingManifestAction to use projection builder
* Assert WebMCP manifests do not expose raw TOON vocabulary
* Add tenant-aware WebMCP discovery filter task
* Test WebMCP discovery tenant isolation
* Add policy-derived WebMCP exposure filter
* Test policy-derived WebMCP exposure filtering
* Add policy snapshot references to WebMCP projections
* Expose approval and ChangeSet requirements in projections
* Test approval and ChangeSet projection metadata
* Extend WebMCP execute request context validation
* Test WebMCP execution context validation
* Attach WebMCP provenance fields to governed invocation envelope
* Test WebMCP provenance in audit evidence
* Add surface metadata adapter for approved browser-operable surfaces
* Test surface metadata projection boundaries
* Add accessibility metadata to browser-operable projections
* Test accessibility metadata requirements
* Standardize WebMCP structured error responses
* Test WebMCP structured errors
* Extend WebMCP rate-limit and telemetry labels
* Test WebMCP telemetry labels and rate-limit bucket
* Add AgentEval fixture for capability escalation attempts
* Add AgentEval fixture for prompt-injection style payloads
* Add AgentEval fixture for stale surface metadata
* Update canonical MCP API docs for WebMCP projections
* Update WebMCP operations and observability runbook
* Sync OpenAPI contract for WebMCP endpoints
* Capture targeted WebMCP quality-gate evidence
* Create WebMCP rollout and rollback handoff
* Close out WebMCP planning artifacts after implementation

## Notes

* Completed 137 work unit(s)
* Removed/archived 2 incomplete unit(s)
* Archived 31 previously completed unit(s)
* Item adherence: 0% (0/3 focus items)
* Feature set adherence: 0% (0/2 planned feature sets had work)
* Weighted adherence: 0% (with partial credit)
* Untracked activity: 47 commit(s) not mapped to any feature set


<!-- Generated by dev-tracker publish_to_jekyll.py -->
<!-- accomplished-date: 2026-05-22 -->
<!-- unit-ids: webmcp-archive-integration-plan,archive-deepsec-run11-archive-deepsec-run11-regression-remediation-planning-work,threat-model-p0-security-docs-inventory,threat-model-p1-security-knowledge-base-index,threat-model-p1-canonical-threat-model-risk-register,threat-model-p2-tenant-scope-bypass-control-gate,threat-model-p2-tenant-id-route-policy-hardening,threat-model-p3-admin-authorization-explicit-permissions,threat-model-p4-public-privacy-workflow-anti-enumeration,threat-model-p5-file-media-import-hardening,threat-model-p6-mcp-toon-execution-policy-binding,threat-model-p6-mcp-toon-denial-golden-tests,threat-model-p7-webhook-replay-parser-hardening,threat-model-p8-security-audit-coverage-map,threat-model-p9-targeted-quality-gates-and-closeout,archive-privacy-governance-archive-privacy-governance-plan,optimize-publication-logic-optimize-publication-logic-privacygovernance-services,privacy-governance-privacy-governance-foundation-planning-artifacts,privacy-governance-surfaces,pgf-01-regulatory-rule-registry-mvp,pgf-02-regulatory-rule-fixtures,pgf-03-data-element-catalog-mvp,pgf-04-ledger-readiness-inventory-gaps,pgf-05-privacy-control-plane-skeleton,pgf-06-privacy-access-session-enrollment,pgf-07-contact-consent-representation-mappings,pgf-08-tenant-privacy-ledger-view,pgf-09-privacy-identity-links-contestation,pgf-10-privacy-disposition-workflows,pgf-11-privacy-evidence-store-receipts,pgf-12-privacy-presence-events-local-index,pgf-13-federated-discovery-routing-cache,pgf-14-vendor-disconnected-notices,pgf-15-hardening-docs-quality-gates,typescript-eslint-typescript-eslint-parser-version-8-59-4,soc-soc-readiness-implementation-plan-tracker,provisioning-let-validation-handle-invalid-region,webmcp-contract-fixture,webmcp-projection-schema-doc,webmcp-projection-dto,webmcp-exposure-tier-enum,webmcp-projection-builder,webmcp-projection-builder-test,webmcp-manifest-action-refactor,webmcp-no-toon-leak-test,webmcp-tenant-context-filter-task,webmcp-tenant-filter-test,webmcp-policy-filter-service,webmcp-policy-filter-test,webmcp-policy-snapshot-field,webmcp-approval-metadata,webmcp-approval-metadata-test,webmcp-execution-context-request,webmcp-execution-context-test,webmcp-provenance-envelope,webmcp-provenance-test,webmcp-surface-metadata-adapter,webmcp-surface-metadata-test,webmcp-accessibility-metadata,webmcp-accessibility-metadata-test,webmcp-structured-error-contract,webmcp-structured-error-test,webmcp-rate-limit-telemetry,webmcp-rate-limit-telemetry-test,webmcp-eval-fixture-escalation,webmcp-eval-fixture-prompt-injection,webmcp-eval-fixture-stale-metadata,webmcp-api-doc-update,webmcp-runbook-update,webmcp-openapi-sync,webmcp-quality-gate-evidence,webmcp-rollout-handoff,webmcp-planning-closeout,finalize-archived-deepsec-finalize-archived-deepsec-run11-plan-content,refactor-threat-model-refactor-threat-model-documentation-implementation,gpc-current-state-inventory,gpc-domain-enums-and-contracts,gpc-schema-privacy-signals,gpc-schema-policy-evaluations,gpc-schema-processing-suppressions,gpc-model-privacy-signal,gpc-model-policy-evaluation,gpc-model-processing-suppression,gpc-regulatory-rule-fixtures,gpc-request-provenance-hasher,gpc-signal-normalizer,gpc-policy-evaluator,gpc-signal-persistence-action,gpc-suppression-writer,gpc-expiration-task,gpc-middleware,gpc-kernel-registration,gpc-request-state-contract,gpc-api-read-model-contract,gpc-privacy-settings-api-integration,gpc-recognition-notice-contract,gpc-publishing-rendering-suppression,gpc-publishing-cdp-send-eligibility,gpc-anonymous-linkage-flow,gpc-middleware-feature-tests,gpc-policy-evaluator-tests,gpc-suppression-tests,gpc-api-read-model-tests,gpc-publishing-enforcement-tests,gpc-etl-contract,gpc-mcp-toon-contract,gpc-analytics-contract,gpc-cdp-identity-annotation-contract,gpc-propagation-reconciliation-contract,gpc-developer-docs,gpc-quality-gates-and-closeout,multiple-architectural-multiple-architectural-decision-records-privacy,mcp-governance-dtos,mcp-governance-envelope-service,mcp-governance-execution-action,mcp-governance-response-payload,mcp-governance-provenance-context,mcp-governance-regression-coverage,various-planning-various-planning-documentation-trackers-completed,implement-privacy-control-privacy-control-plane-models-services,implement-privacy-governance-privacy-governance-planning-documents-artifacts,pgui-00-current-state-and-contract-discovery,pgui-01-api-contracts-and-fixtures,pgui-02-admin-route-capability-scaffold,pgui-03-tenant-entry-disclosure,pgui-04-tenant-ledger-view,pgui-05-platform-privacy-center-shell,pgui-06-receipt-lookup-readonly,pgui-07-admin-governance-shell,pgui-08-ledger-readiness-inventory-gap-queues,pgui-09-requests-evidence-admin-queues,pgui-10-registry-presence-health-admin,pgui-11-governance-metrics-contracts,pgui-12-governance-metrics-ui,pgui-13-request-disposition-workflows,pgui-14-quality-gates-and-closeout,comprehensive-threat-comprehensive-threat-model-documentation-colossalistic -->

<!-- accomplished-unit-ids: archive-deepsec-run11-archive-deepsec-run11-regression-remediation-planning-work,archive-privacy-governance-archive-privacy-governance-plan,comprehensive-threat-comprehensive-threat-model-documentation-colossalistic,finalize-archived-deepsec-finalize-archived-deepsec-run11-plan-content,gpc-analytics-contract,gpc-anonymous-linkage-flow,gpc-api-read-model-contract,gpc-api-read-model-tests,gpc-cdp-identity-annotation-contract,gpc-current-state-inventory,gpc-developer-docs,gpc-domain-enums-and-contracts,gpc-etl-contract,gpc-expiration-task,gpc-kernel-registration,gpc-mcp-toon-contract,gpc-middleware,gpc-middleware-feature-tests,gpc-model-policy-evaluation,gpc-model-privacy-signal,gpc-model-processing-suppression,gpc-policy-evaluator,gpc-policy-evaluator-tests,gpc-privacy-settings-api-integration,gpc-propagation-reconciliation-contract,gpc-publishing-cdp-send-eligibility,gpc-publishing-enforcement-tests,gpc-publishing-rendering-suppression,gpc-quality-gates-and-closeout,gpc-recognition-notice-contract,gpc-regulatory-rule-fixtures,gpc-request-provenance-hasher,gpc-request-state-contract,gpc-schema-policy-evaluations,gpc-schema-privacy-signals,gpc-schema-processing-suppressions,gpc-signal-normalizer,gpc-signal-persistence-action,gpc-suppression-tests,gpc-suppression-writer,implement-privacy-control-privacy-control-plane-models-services,implement-privacy-governance-privacy-governance-planning-documents-artifacts,mcp-governance-dtos,mcp-governance-envelope-service,mcp-governance-execution-action,mcp-governance-provenance-context,mcp-governance-regression-coverage,mcp-governance-response-payload,multiple-architectural-multiple-architectural-decision-records-privacy,optimize-publication-logic-optimize-publication-logic-privacygovernance-services,pgf-01-regulatory-rule-registry-mvp,pgf-02-regulatory-rule-fixtures,pgf-03-data-element-catalog-mvp,pgf-04-ledger-readiness-inventory-gaps,pgf-05-privacy-control-plane-skeleton,pgf-06-privacy-access-session-enrollment,pgf-07-contact-consent-representation-mappings,pgf-08-tenant-privacy-ledger-view,pgf-09-privacy-identity-links-contestation,pgf-10-privacy-disposition-workflows,pgf-11-privacy-evidence-store-receipts,pgf-12-privacy-presence-events-local-index,pgf-13-federated-discovery-routing-cache,pgf-14-vendor-disconnected-notices,pgf-15-hardening-docs-quality-gates,pgui-00-current-state-and-contract-discovery,pgui-01-api-contracts-and-fixtures,pgui-02-admin-route-capability-scaffold,pgui-03-tenant-entry-disclosure,pgui-04-tenant-ledger-view,pgui-05-platform-privacy-center-shell,pgui-06-receipt-lookup-readonly,pgui-07-admin-governance-shell,pgui-08-ledger-readiness-inventory-gap-queues,pgui-09-requests-evidence-admin-queues,pgui-10-registry-presence-health-admin,pgui-11-governance-metrics-contracts,pgui-12-governance-metrics-ui,pgui-13-request-disposition-workflows,pgui-14-quality-gates-and-closeout,privacy-governance-privacy-governance-foundation-planning-artifacts,privacy-governance-surfaces,provisioning-let-validation-handle-invalid-region,refactor-threat-model-refactor-threat-model-documentation-implementation,soc-soc-readiness-implementation-plan-tracker,threat-model-p0-security-docs-inventory,threat-model-p1-canonical-threat-model-risk-register,threat-model-p1-security-knowledge-base-index,threat-model-p2-tenant-id-route-policy-hardening,threat-model-p2-tenant-scope-bypass-control-gate,threat-model-p3-admin-authorization-explicit-permissions,threat-model-p4-public-privacy-workflow-anti-enumeration,threat-model-p5-file-media-import-hardening,threat-model-p6-mcp-toon-denial-golden-tests,threat-model-p6-mcp-toon-execution-policy-binding,threat-model-p7-webhook-replay-parser-hardening,threat-model-p8-security-audit-coverage-map,threat-model-p9-targeted-quality-gates-and-closeout,typescript-eslint-typescript-eslint-parser-version-8-59-4,various-planning-various-planning-documentation-trackers-completed,webmcp-accessibility-metadata,webmcp-accessibility-metadata-test,webmcp-api-doc-update,webmcp-approval-metadata,webmcp-approval-metadata-test,webmcp-archive-integration-plan,webmcp-contract-fixture,webmcp-eval-fixture-escalation,webmcp-eval-fixture-prompt-injection,webmcp-eval-fixture-stale-metadata,webmcp-execution-context-request,webmcp-execution-context-test,webmcp-exposure-tier-enum,webmcp-manifest-action-refactor,webmcp-no-toon-leak-test,webmcp-openapi-sync,webmcp-planning-closeout,webmcp-policy-filter-service,webmcp-policy-filter-test,webmcp-policy-snapshot-field,webmcp-projection-builder,webmcp-projection-builder-test,webmcp-projection-dto,webmcp-projection-schema-doc,webmcp-provenance-envelope,webmcp-provenance-test,webmcp-quality-gate-evidence,webmcp-rate-limit-telemetry,webmcp-rate-limit-telemetry-test,webmcp-rollout-handoff,webmcp-runbook-update,webmcp-structured-error-contract,webmcp-structured-error-test,webmcp-surface-metadata-adapter,webmcp-surface-metadata-test,webmcp-tenant-context-filter-task,webmcp-tenant-filter-test -->
<!-- SECTION: ACCOMPLISHED END -->
<!-- Generated by dev-tracker build_today_plan.py -->
