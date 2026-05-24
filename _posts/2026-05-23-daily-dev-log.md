---
layout: post
title: "Daily Dev Log - 2026-05-23"
date: 2026-05-23
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-05-23T12:48:09.159323+00:00 -->

## Today's Theme

Yesterday I completed 137 items across 22 feature sets - a massive push that wrapped up several major security initiatives including the threat-model work and privacy-governance-foundation. What's bothering me is how I completely deviated from my planned focus areas again. The privacy-orchestration-deletion work I touched in the last 24 hours is pulling at me because it represents genuine compliance infrastructure, not just security theater. The accidental-pint remediation that I've been investing heavily in this week still has those two terrifying cohorts left, and I'm running out of excuses to avoid the billing one.

## The Main Work

**Map the privacy obligation ownership boundaries (podcp-00-source-research-boundary-map)** - This is foundational work for the entire privacy deletion orchestration system, and I can't design obligation schemas without understanding who owns what data. The planning shows this is Phase 0 research, which means I'm still figuring out the basic architecture. I'm genuinely curious how complex the ownership boundaries will be - is this a simple tenant-scoped model or do we have cross-cutting concerns that make deletion coordination genuinely difficult?

**Complete the Core Billing accidental Pint cohort (accidental-pint-core-billing)** - This has been haunting me for weeks because billing code touches invoice generation, payment processing, and customer charges. Any formatting changes that introduce subtle arithmetic bugs or operator precedence issues could affect money calculations in ways that don't surface until customers start calling about wrong bills months later. I'd rather spend the time to be methodical here than discover we've been overcharging people due to a misplaced parenthesis in a Pint auto-fix.

**Clean up the Jest coverage denominator and refresh baseline (frontend-jest-coverage-expansion-denominator-cleanup)** - The coverage metrics are probably inflated with dead components and stale test files, making our actual frontend coverage look worse than it is. This bothers me because I'm making decisions about test investment based on potentially garbage data. The work is marked as active this week, and cleaning up the denominator feels more productive than writing new tests against a broken baseline.

**Add the Privacy Obligation schema and lifecycle taxonomy (podcp-01-obligation-schema-and-lifecycle)** - Once I understand the ownership boundaries, this schema becomes the core contract that everything else builds on. The obligation lifecycle determines how deletion requests flow through the system, and getting this wrong would make the entire privacy orchestration feature either useless for compliance or dangerous for data integrity.

## Housekeeping

**Regenerate the PHPStan baseline after recent security work** - With 13,196 errors at level 9, the baseline is probably stale after yesterday's massive security push across multiple feature sets. Running `make phpstan-baseline` will capture the current state and give me a clean foundation for future improvements.

**Draft implementation plan for california-compliance-audit** - This planning directory aligns with the privacy work I'm already deep in, and the compliance context is fresh from all the security remediation. The tracker shows it needs a plan, and I can advance this while the privacy orchestration concepts are loaded in my brain.

**Fix 3-5 markdownlint issues in docs I'm already touching** - The 196 issues across 12 files include documentation I'll be updating for the privacy work anyway. Better to clean up formatting violations in files I'm already editing than let them accumulate.

**Review the test harness inventory for privacy-related gaps** - The test-harness-ci-manifest planning shows 9 work units ready, and I should identify any privacy-specific test coverage holes while I'm building out the obligation schema.

## Parked

The Core ETL accidental Pint cohort can wait another day - it's less risky than the billing work and I'd rather tackle the money-touching code while my attention is sharp. The horizontal slice HS126 work is nearly complete but it's not urgent compared to the compliance infrastructure that could actually protect us in an audit.

<!-- plan-unit-ids: accidental-pint-core-billing,accidental-pint-core-tenancy,todoremed-p0-replace-template-boilerplate -->
<!-- SECTION: DAILY-PLAN END -->


<!-- SECTION: ACCOMPLISHED START -->
<!-- accomplished-generated: 2026-05-24T13:23:44.486090+00:00 -->
<!-- accomplished-updated: 2026-05-24T13:23:44.486090+00:00 -->

* Completed 167 tasks today on the Colossalistic Platform project.

## What I Built

### analytics-gpc-downgrade
* Inventory analytics sources, sinks, and transformations
* Define analytics downgrade policy contract
* Enforce downgrade at event collection and export boundaries
* Enforce downgrade for features, audiences, and model inputs
* Add evidence and reconciliation reporting
* Publish docs and run targeted quality gates

### cali-readiness-imp
* Define neutral control envelope and adapter contract
* Implement neutral registry and adapter discovery
* Migrate SOC 2 definitions and validation to adapter shape
* Implement neutral materialization, evaluation, and export orchestration
* Migrate SOC 2 API and docs to neutral control surface
* Add immediate framework dependency-direction guard
* Add California control adapter and definition validator
* Publish CA-PRIVACY control definitions
* Expose California control evaluation and export path
* Apply GPC suppression to ETL export and sync eligibility
* Annotate CDP contact and identity read models with tenant-local GPC state
* Record first-wave GPC propagation reconciliation evidence
* Create canonical California SPI category vocabulary
* Attach California SPI categories to Data Element Catalog entries
* Add source-domain SPI evidence reconciliation
* Expand deletion processor capability map
* Implement concrete deletion adapters where source APIs exist
* Create ADMT and profiling inventory contract
* Map California risk assessment and cybersecurity audit readiness
* Add data broker and DROP classification gate
* Run targeted quality gates and close out planning artifacts

### california-compliance-audit
* Inventory source material and existing privacy foundations
* Establish official California citation baseline
* Define California privacy control taxonomy
* Audit CPRA/CCPA consumer rights controls
* Audit Global Privacy Control enforcement controls
* Audit sensitive personal information classification and handling
* Audit data minimization, purpose limitation, and retention controls
* Audit deletion orchestration and receipt controls
* Audit dark-pattern and choice-symmetry risks
* Audit vendor and processor governance controls
* Audit privacy policy and disclosure accuracy
* Audit California privacy security-overlap controls
* Audit ADMT and profiling readiness controls
* Audit risk assessment and cybersecurity audit readiness
* Audit Delete Act and DROP readiness
* Audit data broker adjacency and cross-tenant intelligence risk
* Audit AI memory and agent governance readiness
* Audit residency and sovereignty readiness
* Create California privacy evidence source map
* Create California regulatory readiness matrix
* Create remediation backlog and follow-up slice map
* Create platform compliance map
* Review audit findings with engineering, compliance, and product
* Create canonical documentation promotion plan
* Keep tracker and checklist synchronized
* Run targeted quality gates for touched audit files
* Prepare planning close-out disposition

### california-readiness
* Update California readiness artifacts and implementation checklist

### drop-implementation
* Create data broker classification baseline
* Design DROP account, credential, and list ingestion path
* Define subject matching and identity resolution contract
* Route DROP obligations through PrivacyControlPlane
* Expand processor capability coverage for DROP
* Implement status reporting and Compliance evidence
* Publish docs and run targeted quality gates

### mcp-toon-gpc-enforcement
* Confirm MCP/TOON GPC contract baseline
* Define Compliance GPC enforcement context Interface
* Implement MCP pre-invocation guard
* Wire TOON policy and provenance decisions
* Add derived output downgrade and redaction behavior
* Materialize GPC enforcement evidence
* Run targeted tests, docs, and quality gates

### migration-squash-recovery
* chore(db): resolve duplicate policy_reviews migration
* fix(db): drop redundant Closure use in postmark migration
* chore(db): remove migration-squash baseline machinery
* chore(db): consolidate migrations into laravel-app/database/migrations/
* fix(db): widen age_gate_records.user_agent to TEXT
* fix(db): add void return types to login_history migration
* fix(db): drop redundant index on usage_raw.event_hash
* fix(db): drop redundant index on customer_budget_configurations.customer_id
* fix(db): use IS TRUE for boolean predicate in users partial index
* fix(db): index plan and status on billing_accounts alter path
* fix(db): drop redundant index on accessibility_alert_stats.date
* fix(db): drop redundant composite index on system_settings
* fix(db): add tenant scoping to remaining shopify_test entity tables
* fix(db): stream finops_report tag-filter backfill via chunkById
* fix(db): skip redundant customer/recorded_at index when prefix covers it
* fix(db): add void return type to domains Schema::create closure
* fix(db): add void return type to billing_accounts Schema::table closure
* fix(db): add void return types to remaining legal_entities closures
* fix(db): add void return type to integration_configs Schema::create closure
* fix(db): add void return type to idempotency_keys Schema::create closure
* style(db): add void return type to Blueprint closures (2026_05 bucket)
* style(db): add void return type to Blueprint closures (2025_01 bucket)
* style(db): add void return type to Blueprint closures (2025_05 bucket)
* style(db): add void return type to Blueprint closures (2025_06 bucket)
* style(db): add void return type to Blueprint closures (2025_07 bucket)
* style(db): add void return type to Blueprint closures (2025_09 bucket)
* style(db): add void return type to Blueprint closures (2025_10 bucket)
* style(db): add void return type to Blueprint closures (2025_11 bucket)
* style(db): add void return type to Blueprint closures (2025_12 bucket)
* style(db): add void return type to Blueprint closures (2026_01 bucket)
* style(db): add void return type to Blueprint closures (2026_02 bucket)
* style(db): add void return type to Blueprint closures (2026_03 bucket)
* fix(db): add FK on user_security_flags.threat_detection_id
* fix(db): add FK on security_ip_blacklist.threat_detection_id
* fix(db): drop redundant index on mcp_chat_sessions.session_id
* fix(db): drop redundant index on mcp_ai_agents.slug
* fix(db): make email_webhook_events.processed_at nullable
* fix(db): restrict deletion of email_contact_lists with active campaigns
* fix(db): tenant-scope surface_action_logs -> surface_instances FK
* fix(db): strip operational side effects from JWT-rotate migration
* fix(db): strip .env mutation from add_coppa_jwt_secret_to_env
* fix(db): make integration_configs migration self-consistent with its tenant claim
* fix(db): add void return types to email_service_configs migration
* fix(db): add atomicity guard to pricing_engine rollback
* fix(db): pricing_engine down() throws on partial state instead of silently returning
* fix(db): narrow filters typing + sub-chunk inserts in finops tag-filter backfill
* fix(db): guard crm_sync_logs analytics-index migration with hasTable

### privacy-orchestration-deletion
* Document source research and ownership boundaries
* Add Privacy Obligation schema, models, and lifecycle taxonomy
* Normalize privacy signals into executable obligation drafts
* Resolve policy, jurisdiction, and retention conflicts before execution
* Discover authoritative deletion targets from provenance and representations
* Create processor capability registry and adapter interface
* Implement first internal deletion processors
* Add obligation execution jobs, retries, and dead-letter handling
* Generate evidence, receipts, and completion validation
* Run targeted quality gates and prepare planning close-out
* Expose backend API and event contracts for future UI expansion
* Add privacy orchestration evaluation and security tests
* Publish canonical docs and operational runbooks

### refactor-california-compliance
* Refactor California Compliance Audit documentation  and tracker

### soc-readiness
* Define SOC 2 control definition schema
* Add five initial SOC 2 control fixtures
* Test SOC 2 control fixture validation
* Create compliance controls migration
* Create compliance evidence records migration
* Create compliance control evaluations migration
* Create ComplianceControl model and factory
* Create ComplianceEvidenceRecord model and factory
* Create ComplianceControlEvaluation model and factory
* Implement SOC 2 control registry loader
* Test SOC 2 control registry loader
* Define normalized evidence source contracts
* Implement RBAC audit evidence adapter
* Implement TrustFabric policy decision evidence adapter
* Implement AgentEval evidence adapter
* Implement provenance ledger evidence adapter
* Implement tenant isolation evidence adapter
* Implement canonical evidence hash service
* Implement evidence materialization action
* Test evidence materialization
* Test sealed evidence immutability
* Implement deterministic control evaluation service
* Implement control evaluation action
* Test deterministic control evaluation outcomes
* Create SOC readiness admin Form Requests
* Create SOC readiness API resources
* Add SOC readiness admin controller and routes
* Update CompliancePolicy for SOC readiness permissions
* Test SOC readiness admin API
* Test SOC readiness cross-tenant isolation
* Implement JSON evidence manifest export
* Test evidence manifest redaction
* Write canonical SOC readiness API documentation
* Write SOC readiness operations runbook
* Document Compliance Control Plane authority boundary
* Run targeted SOC readiness quality gates
* Archive SOC readiness implementation evidence

## Progress Made

* Publish ADR-0255 for UCP projection boundary (in progress)
* Scaffold Core/CommerceCheckout Porto container (in progress)
* Create checkout aggregate, line item, and event migrations (in progress)
* Implement Commerce Checkout models and factories (in progress)
* Implement checkout state machine and transition guards (in progress)
* Implement create checkout action and task flow (in progress)
* Implement complete checkout action and completion record (in progress)
* Add Form Requests for checkout APIs (in progress)
* Expose canonical governed MCP checkout routes (in progress)
* Register Commerce Checkout MCP tool definitions (in progress)
* Wire Commerce Checkout TOON capability checks (in progress)
* Map UCP checkout aliases through AgentInterface (in progress)
* Implement Checkout Request Fingerprint and idempotency wrapper (in progress)
* Integrate idempotency into mutating checkout tools (in progress)
* Capture policy decision and governed invocation context (in progress)
* Finalize append-only checkout audit event contract (in progress)
* Run and record targeted quality gates (in progress)
* Define pinned UCP checkout.v1 compatibility profile schemas (in progress)
* Implement get checkout action and task flow (in progress)
* Gate UCP checkout invocation to internal agents for Phase 1 (in progress)
* Add UCP profile configuration (in progress)
* Add checkout DTOs, resources, and error envelope mapping (in progress)
* Implement update checkout action and task flow (in progress)
* Implement cancel and expire checkout flows (in progress)
* Add route parity and discovery regression coverage (in progress)
* Add Commerce Checkout container README (in progress)

## Notes

* Completed 167 work unit(s)
* Made progress on 26 work unit(s)
* Item adherence: 0% (0/3 focus items)
* Feature set adherence: 0% (0/2 planned feature sets had work)
* Weighted adherence: 33% (with partial credit)
* Untracked activity: 84 commit(s) not mapped to any feature set
* Auto-archived 1 retroactive feature sets from untracked commits


<!-- Generated by dev-tracker publish_to_jekyll.py -->
<!-- accomplished-date: 2026-05-23 -->
<!-- unit-ids: podcp-00-source-research-boundary-map,podcp-01-obligation-schema-and-lifecycle,podcp-02-signal-normalization-contracts,podcp-03-policy-resolution-and-conflict-gates,podcp-04-provenance-target-discovery,podcp-05-processor-capability-registry,podcp-06-internal-processor-execution,podcp-07-obligation-execution-jobs-and-dlq,podcp-08-evidence-receipt-and-completion-validation,podcp-12-targeted-quality-gates-and-closeout,podcp-09-api-and-event-contracts-for-future-ui,podcp-10-evaluation-and-security-regression-suite,podcp-11-canonical-docs-and-runbooks,drop-classification-baseline,drop-ingestion-design,drop-subject-matching,drop-obligation-orchestration,drop-processor-capabilities,drop-status-evidence,drop-docs-quality,analytics-gpc-inventory-baseline,analytics-gpc-downgrade-policy,analytics-gpc-event-enforcement,analytics-gpc-feature-enforcement,analytics-gpc-evidence-reconciliation,analytics-gpc-docs-quality,cali-neutral-envelope-adapter-contract,cali-neutral-registry-adapter-discovery,cali-neutral-soc2-adapter-migration,cali-neutral-materialization-evaluation-export,cali-neutral-api-docs-migration,cali-neutral-dependency-direction-guard,cali-control-definition-validator,cali-control-definitions,cali-control-api-and-export,cali-gpc-etl-enforcement,cali-gpc-cdp-annotation,cali-gpc-reconciliation-evidence,cali-spi-category-vocabulary,cali-spi-catalog-attachments,cali-spi-source-evidence-reconciliation,cali-deletion-processor-capability-map,cali-deletion-supported-adapters,cali-admt-profiling-inventory,cali-risk-and-cyber-readiness,cali-data-broker-drop-gate,cali-quality-gates-and-closeout,soc2-control-definition-schema,soc2-initial-control-fixtures,soc2-control-fixture-validation-test,soc2-compliance-controls-migration,soc2-evidence-records-migration,soc2-control-evaluations-migration,soc2-compliance-control-model,soc2-evidence-record-model,soc2-control-evaluation-model,soc2-control-registry-loader,soc2-control-registry-loader-test,soc2-evidence-source-contracts,soc2-rbac-evidence-adapter,soc2-trustfabric-evidence-adapter,soc2-agenteval-evidence-adapter,soc2-provenance-evidence-adapter,soc2-tenant-isolation-evidence-adapter,soc2-evidence-canonical-hasher,soc2-evidence-materialization-action,soc2-evidence-materialization-test,soc2-evidence-immutability-test,soc2-control-evaluation-service,soc2-control-evaluation-action,soc2-control-evaluation-tests,soc2-admin-request-classes,soc2-admin-resources,soc2-admin-controller-routes,soc2-compliance-policy-updates,soc2-admin-api-feature-tests,soc2-cross-tenant-isolation-tests,soc2-json-evidence-manifest-export,soc2-export-redaction-tests,soc2-canonical-api-docs,soc2-operations-runbook,soc2-architecture-boundary-doc,soc2-targeted-quality-gates,soc2-planning-closeout-evidence,mcp-toon-gpc-contract-baseline,mcp-toon-gpc-compliance-interface,mcp-toon-gpc-mcp-guard,mcp-toon-gpc-toon-provenance,mcp-toon-gpc-derived-output,mcp-toon-gpc-evidence,mcp-toon-gpc-quality-gates,california-readiness-california-readiness-artifacts-implementation-checklist,ca-audit-source-inventory,ca-audit-official-citation-baseline,ca-audit-control-taxonomy,ca-audit-current-cpra-rights,ca-audit-gpc-controls,ca-audit-sensitive-personal-information,ca-audit-minimization-retention,ca-audit-deletion-orchestration,ca-audit-dark-patterns,ca-audit-vendor-processor-governance,ca-audit-disclosure-accuracy,ca-audit-security-overlap,ca-audit-admt-readiness,ca-audit-risk-assessment-cyber-readiness,ca-audit-delete-act-drop-readiness,ca-audit-data-broker-adjacency,ca-audit-ai-memory-governance,ca-audit-residency-sovereignty-readiness,ca-audit-evidence-source-map,ca-audit-readiness-matrix,ca-audit-remediation-backlog,ca-audit-platform-compliance-map,ca-audit-review-with-stakeholders,ca-audit-canonical-doc-promotion-plan,ca-audit-tracker-checklist-sync,ca-audit-targeted-quality-gates,ca-audit-closeout-disposition,refactor-california-compliance-refactor-california-compliance-audit-documentation,msr-b7521ac-resolve-duplicate-policy-reviews-migration,msr-e963adc-drop-redundant-closure-use-in-postmark-migration,msr-239852a-remove-migration-squash-baseline-machinery,msr-cc49268-consolidate-migrations-into-laravel-app-database-migrations,msr-4a8528e-widen-age-gate-records-user-agent-to-text,msr-f5c798b-add-void-return-types-to-login-history-migration,msr-056f914-drop-redundant-index-on-usage-raw-event-hash,msr-757230f-drop-redundant-index-on-customer-budget-configurations-customer-id,msr-210e174-use-is-true-for-boolean-predicate-in-users-partial-index,msr-1b69212-index-plan-and-status-on-billing-accounts-alter-path,msr-5446d22-drop-redundant-index-on-accessibility-alert-stats-date,msr-02963ee-drop-redundant-composite-index-on-system-settings,msr-4d3a5c8-add-tenant-scoping-to-remaining-shopify-test-entity-tables,msr-65edf6a-stream-finops-report-tag-filter-backfill-via-chunkbyid,msr-c613223-skip-redundant-customer-recorded-at-index-when-prefix-covers-it,msr-3d1ab3b-add-void-return-type-to-domains-schema-create-closure,msr-124176d-add-void-return-type-to-billing-accounts-schema-table-closure,msr-411d009-add-void-return-types-to-remaining-legal-entities-closures,msr-727ff4c-add-void-return-type-to-integration-configs-schema-create-closure,msr-01b5dbd-add-void-return-type-to-idempotency-keys-schema-create-closure,msr-68e0f57-add-void-return-type-to-blueprint-closures-2026-05-bucket,msr-bc5026b-add-void-return-type-to-blueprint-closures-2025-01-bucket,msr-d2ff009-add-void-return-type-to-blueprint-closures-2025-05-bucket,msr-65ed2f7-add-void-return-type-to-blueprint-closures-2025-06-bucket,msr-1dc5eec-add-void-return-type-to-blueprint-closures-2025-07-bucket,msr-e43a692-add-void-return-type-to-blueprint-closures-2025-09-bucket,msr-70b75e4-add-void-return-type-to-blueprint-closures-2025-10-bucket,msr-af024a9-add-void-return-type-to-blueprint-closures-2025-11-bucket,msr-9a0b445-add-void-return-type-to-blueprint-closures-2025-12-bucket,msr-609ba6f-add-void-return-type-to-blueprint-closures-2026-01-bucket,msr-27c680c-add-void-return-type-to-blueprint-closures-2026-02-bucket,msr-9ebb079-add-void-return-type-to-blueprint-closures-2026-03-bucket,msr-e8b20cc-add-fk-on-user-security-flags-threat-detection-id,msr-989d2ba-add-fk-on-security-ip-blacklist-threat-detection-id,msr-07d51db-drop-redundant-index-on-mcp-chat-sessions-session-id,msr-c6b24d2-drop-redundant-index-on-mcp-ai-agents-slug,msr-43b132a-make-email-webhook-events-processed-at-nullable,msr-720e349-restrict-deletion-of-email-contact-lists-with-active-campaigns,msr-cc17fe6-tenant-scope-surface-action-logs-surface-instances-fk,msr-fa625a8-strip-operational-side-effects-from-jwt-rotate-migration,msr-ee68eaa-strip-env-mutation-from-add-coppa-jwt-secret-to-env,msr-1057e26-make-integration-configs-migration-self-consistent-with-its-tenant-claim,msr-f7c2534-add-void-return-types-to-email-service-configs-migration,msr-c1d2e46-add-atomicity-guard-to-pricing-engine-rollback,msr-d71a348-pricing-engine-down-throws-on-partial-state-instead-of-silently-returning,msr-a890aa0-narrow-filters-typing-sub-chunk-inserts-in-finops-tag-filter-backfill,msr-e40d99d-guard-crm-sync-logs-analytics-index-migration-with-hastable -->

<!-- accomplished-unit-ids: analytics-gpc-docs-quality,analytics-gpc-downgrade-policy,analytics-gpc-event-enforcement,analytics-gpc-evidence-reconciliation,analytics-gpc-feature-enforcement,analytics-gpc-inventory-baseline,ca-audit-admt-readiness,ca-audit-ai-memory-governance,ca-audit-canonical-doc-promotion-plan,ca-audit-closeout-disposition,ca-audit-control-taxonomy,ca-audit-current-cpra-rights,ca-audit-dark-patterns,ca-audit-data-broker-adjacency,ca-audit-delete-act-drop-readiness,ca-audit-deletion-orchestration,ca-audit-disclosure-accuracy,ca-audit-evidence-source-map,ca-audit-gpc-controls,ca-audit-minimization-retention,ca-audit-official-citation-baseline,ca-audit-platform-compliance-map,ca-audit-readiness-matrix,ca-audit-remediation-backlog,ca-audit-residency-sovereignty-readiness,ca-audit-review-with-stakeholders,ca-audit-risk-assessment-cyber-readiness,ca-audit-security-overlap,ca-audit-sensitive-personal-information,ca-audit-source-inventory,ca-audit-targeted-quality-gates,ca-audit-tracker-checklist-sync,ca-audit-vendor-processor-governance,cali-admt-profiling-inventory,cali-control-api-and-export,cali-control-definition-validator,cali-control-definitions,cali-data-broker-drop-gate,cali-deletion-processor-capability-map,cali-deletion-supported-adapters,cali-gpc-cdp-annotation,cali-gpc-etl-enforcement,cali-gpc-reconciliation-evidence,cali-neutral-api-docs-migration,cali-neutral-dependency-direction-guard,cali-neutral-envelope-adapter-contract,cali-neutral-materialization-evaluation-export,cali-neutral-registry-adapter-discovery,cali-neutral-soc2-adapter-migration,cali-quality-gates-and-closeout,cali-risk-and-cyber-readiness,cali-spi-catalog-attachments,cali-spi-category-vocabulary,cali-spi-source-evidence-reconciliation,california-readiness-california-readiness-artifacts-implementation-checklist,drop-classification-baseline,drop-docs-quality,drop-ingestion-design,drop-obligation-orchestration,drop-processor-capabilities,drop-status-evidence,drop-subject-matching,mcp-toon-gpc-compliance-interface,mcp-toon-gpc-contract-baseline,mcp-toon-gpc-derived-output,mcp-toon-gpc-evidence,mcp-toon-gpc-mcp-guard,mcp-toon-gpc-quality-gates,mcp-toon-gpc-toon-provenance,msr-01b5dbd-add-void-return-type-to-idempotency-keys-schema-create-closure,msr-02963ee-drop-redundant-composite-index-on-system-settings,msr-056f914-drop-redundant-index-on-usage-raw-event-hash,msr-07d51db-drop-redundant-index-on-mcp-chat-sessions-session-id,msr-1057e26-make-integration-configs-migration-self-consistent-with-its-tenant-claim,msr-124176d-add-void-return-type-to-billing-accounts-schema-table-closure,msr-1b69212-index-plan-and-status-on-billing-accounts-alter-path,msr-1dc5eec-add-void-return-type-to-blueprint-closures-2025-07-bucket,msr-210e174-use-is-true-for-boolean-predicate-in-users-partial-index,msr-239852a-remove-migration-squash-baseline-machinery,msr-27c680c-add-void-return-type-to-blueprint-closures-2026-02-bucket,msr-3d1ab3b-add-void-return-type-to-domains-schema-create-closure,msr-411d009-add-void-return-types-to-remaining-legal-entities-closures,msr-43b132a-make-email-webhook-events-processed-at-nullable,msr-4a8528e-widen-age-gate-records-user-agent-to-text,msr-4d3a5c8-add-tenant-scoping-to-remaining-shopify-test-entity-tables,msr-5446d22-drop-redundant-index-on-accessibility-alert-stats-date,msr-609ba6f-add-void-return-type-to-blueprint-closures-2026-01-bucket,msr-65ed2f7-add-void-return-type-to-blueprint-closures-2025-06-bucket,msr-65edf6a-stream-finops-report-tag-filter-backfill-via-chunkbyid,msr-68e0f57-add-void-return-type-to-blueprint-closures-2026-05-bucket,msr-70b75e4-add-void-return-type-to-blueprint-closures-2025-10-bucket,msr-720e349-restrict-deletion-of-email-contact-lists-with-active-campaigns,msr-727ff4c-add-void-return-type-to-integration-configs-schema-create-closure,msr-757230f-drop-redundant-index-on-customer-budget-configurations-customer-id,msr-989d2ba-add-fk-on-security-ip-blacklist-threat-detection-id,msr-9a0b445-add-void-return-type-to-blueprint-closures-2025-12-bucket,msr-9ebb079-add-void-return-type-to-blueprint-closures-2026-03-bucket,msr-a890aa0-narrow-filters-typing-sub-chunk-inserts-in-finops-tag-filter-backfill,msr-af024a9-add-void-return-type-to-blueprint-closures-2025-11-bucket,msr-b7521ac-resolve-duplicate-policy-reviews-migration,msr-bc5026b-add-void-return-type-to-blueprint-closures-2025-01-bucket,msr-c1d2e46-add-atomicity-guard-to-pricing-engine-rollback,msr-c613223-skip-redundant-customer-recorded-at-index-when-prefix-covers-it,msr-c6b24d2-drop-redundant-index-on-mcp-ai-agents-slug,msr-cc17fe6-tenant-scope-surface-action-logs-surface-instances-fk,msr-cc49268-consolidate-migrations-into-laravel-app-database-migrations,msr-d2ff009-add-void-return-type-to-blueprint-closures-2025-05-bucket,msr-d71a348-pricing-engine-down-throws-on-partial-state-instead-of-silently-returning,msr-e40d99d-guard-crm-sync-logs-analytics-index-migration-with-hastable,msr-e43a692-add-void-return-type-to-blueprint-closures-2025-09-bucket,msr-e8b20cc-add-fk-on-user-security-flags-threat-detection-id,msr-e963adc-drop-redundant-closure-use-in-postmark-migration,msr-ee68eaa-strip-env-mutation-from-add-coppa-jwt-secret-to-env,msr-f5c798b-add-void-return-types-to-login-history-migration,msr-f7c2534-add-void-return-types-to-email-service-configs-migration,msr-fa625a8-strip-operational-side-effects-from-jwt-rotate-migration,podcp-00-source-research-boundary-map,podcp-01-obligation-schema-and-lifecycle,podcp-02-signal-normalization-contracts,podcp-03-policy-resolution-and-conflict-gates,podcp-04-provenance-target-discovery,podcp-05-processor-capability-registry,podcp-06-internal-processor-execution,podcp-07-obligation-execution-jobs-and-dlq,podcp-08-evidence-receipt-and-completion-validation,podcp-09-api-and-event-contracts-for-future-ui,podcp-10-evaluation-and-security-regression-suite,podcp-11-canonical-docs-and-runbooks,podcp-12-targeted-quality-gates-and-closeout,refactor-california-compliance-refactor-california-compliance-audit-documentation,soc2-admin-api-feature-tests,soc2-admin-controller-routes,soc2-admin-request-classes,soc2-admin-resources,soc2-agenteval-evidence-adapter,soc2-architecture-boundary-doc,soc2-canonical-api-docs,soc2-compliance-control-model,soc2-compliance-controls-migration,soc2-compliance-policy-updates,soc2-control-definition-schema,soc2-control-evaluation-action,soc2-control-evaluation-model,soc2-control-evaluation-service,soc2-control-evaluation-tests,soc2-control-evaluations-migration,soc2-control-fixture-validation-test,soc2-control-registry-loader,soc2-control-registry-loader-test,soc2-cross-tenant-isolation-tests,soc2-evidence-canonical-hasher,soc2-evidence-immutability-test,soc2-evidence-materialization-action,soc2-evidence-materialization-test,soc2-evidence-record-model,soc2-evidence-records-migration,soc2-evidence-source-contracts,soc2-export-redaction-tests,soc2-initial-control-fixtures,soc2-json-evidence-manifest-export,soc2-operations-runbook,soc2-planning-closeout-evidence,soc2-provenance-evidence-adapter,soc2-rbac-evidence-adapter,soc2-targeted-quality-gates,soc2-tenant-isolation-evidence-adapter,soc2-trustfabric-evidence-adapter -->
<!-- SECTION: ACCOMPLISHED END -->
<!-- Generated by dev-tracker build_today_plan.py -->
