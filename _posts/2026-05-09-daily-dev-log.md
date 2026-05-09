---
layout: post
title: "Daily Dev Log - 2026-05-09"
date: 2026-05-09
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-05-09T13:43:47.762908+00:00 -->

## Today's Theme

I finished the accidental-pint-remediation work yesterday - 12 of 32 items complete with only the Core ETL and Core Billing cohorts left hanging. But what's really pulling me forward today is the tenant context job propagation work I've been circling. The production-readiness implications are keeping me up at night because background jobs without proper tenant isolation could create genuine compliance disasters.

## The Main Work

**Define the MustCarryTenantContext interface in Ship Contracts (tenant-job-interface)** - This forces me to think through which background jobs legitimately need tenant context versus which ones are tenant-agnostic. A billing job that accidentally processes invoices for the wrong customer isn't just a bug - it's a lawsuit waiting to happen. The interface design is the foundation that prevents those 3am pages where you discover data leaked across tenant boundaries.

**Remediate the Core Billing cohort for accidental Pint changes (accidental-pint-core-billing)** - I actually started this yesterday as unplanned work, so the mental model of what needs fixing is still sharp. The billing layer is particularly sensitive because any formatting changes that introduce subtle bugs could affect invoice generation or payment processing. Better to finish this methodically than rush and break money flows.

**Generate the migration guard audit report (migration-guard-audit-script)** - I'm genuinely nervous about how many unguarded Schema::create calls we have lurking in our migrations. If a deployment rolls back partially and then tries to migrate forward again, unguarded creates will brick the database. This audit either shows manageable scope or reveals why our deployment process is more fragile than I want to admit.

**Complete the Core ETL cohort remediation (accidental-pint-core-etl)** - This closes out the formatting mess I've been chipping away at all week. The ETL pipelines touch so much data that I'm paranoid about introducing regressions through cosmetic changes. Once this lands, I can finally archive the accidental-pint-remediation planning directory and stop thinking about it.

## Housekeeping

**Run the stale test suite to refresh PHP test results** - The 89% pass rate is 11 days old, which means I'm flying blind on whether recent changes broke anything. A quick `make test-fixed-batches-quick` will either confirm things are stable or surface regressions that need immediate attention.

**Draft the tenant job middleware implementation plan** - Since I'm deep in the tenant context propagation work, this is a perfect time to outline how the TenantContextJobMiddleware should actually work. The planning pipeline shows this as ready for implementation, and having the approach documented will make the coding phase much smoother.

**Regenerate the route health report** - The 2902 routes with "warning" status is 9 days stale. Running `make sync-routes` takes maybe 10 minutes but gives me current visibility into API surface health, especially important since I'm working on middleware that affects request processing.

## Parked

The migration safety schema guards work is tempting because it's production-critical, but I suspect it's a rabbit hole that could consume the entire day. Once I start auditing Schema::create calls, I'll want to fix everything immediately rather than just cataloging the scope. The audit report comes first - remediation can wait until next week when I have a clearer picture of the actual scale.

<!-- plan-unit-ids: accidental-pint-core-billing,csp-middleware-report-only,migration-guard-audit-script,tenant-job-interface,todoremed-p0-replace-template-boilerplate -->
<!-- SECTION: DAILY-PLAN END -->


<!-- SECTION: ACCOMPLISHED START -->
<!-- accomplished-generated: 2026-05-09T21:14:38.551502+00:00 -->
<!-- accomplished-updated: 2026-05-09T21:14:38.551502+00:00 -->

## Today's Update

Today was fundamentally about building safety nets - across migrations, tenant isolation, and code quality. I tackled three major architectural concerns that have been accumulating technical debt, plus made substantial progress on React component remediation that's been a ongoing project.

The migration safety work was the most comprehensive effort. I built out a complete guard system for our Laravel migrations, starting with an audit script to classify all existing migrations into risk tiers. Then I systematically wrapped tier A Schema::create migrations in hasTable guards across three cohorts - about 150 files total. The tier B column migrations got hasColumn guards, and I individually resolved the tier C edge cases that were mixed schema and backfill operations. The satisfying capstone was adding a custom PHPStan rule that enforces the guard policy going forward, plus extending our nightly CI with a fresh-DB migration job to catch issues early. What I learned is that our migration files had way more inconsistency than I expected - some were defensive, others assumed clean state, and a few were doing schema changes mixed with data operations that really should be separate.

The tenant isolation work was equally systematic but more complex architecturally. I audited every queued job class for tenant context issues and converted them in four cohorts - webhooks and payments first, then email and notifications, ETL and sync jobs, and finally the remaining miscellaneous jobs. Each cohort needed different approaches because they touch tenant data in different ways. I built integration tests proving that the shadow-mode middleware actually isolates tenant context in queued jobs, which was trickier than expected because you have to verify isolation without actually violating it in the test. Added another PHPStan rule to catch future violations, plus a documented allowlist for the few jobs that legitimately don't need tenant context.

I also consolidated the container seeders scattered throughout the Porto architecture into a centralized database/seeders structure. This involved inventorying seeders across all containers, moving them with git mv to preserve history, registering them in DatabaseSeeder with deterministic ordering, and adding a PHPStan rule to prevent future sprawl. The deterministic ordering was important because seeder dependencies can be subtle - you don't want UserSeeder running after RoleSeeder sometimes and before it other times.

The React Doctor remediation continued with both baseline and followup work. I stabilized the inherited react-doctor-fix branch, established repo-level configuration, added shared fetch mock utilities, and applied remediation across selected components. The focus trap utilities for modal enforcement were particularly fiddly because accessibility requirements interact with React's event system in non-obvious ways. I'm still short of the 100/100 target score, so that goal moves to the next sprint.

Finally, I wrapped up the structured logging migration by parsing our Grafana dashboard JSON to identify which log keys are actually being used in production. Turns out we had several dead dashboard panels pointing to log keys that no longer exist - cleaned those up and produced a coverage map showing which parts of the logging surface are monitored versus just noise.

This foundation work removes a lot of operational risk and sets up cleaner development workflows. The migration guards alone should prevent the kind of production schema issues we've seen when engineers assume clean database state.

**The Numbers:**
- Completed: 56 tasks  
- Feature areas: react-doctor-100-followup-sprint, migration-safety-schema-guards, tenant-context-job-propagation, container-seeders-consolidation, cross-tenant-isolation-test-suite, react-doctor-baseline-remediation, structured-logging-final-wave, react-doctor, tenant-aware, loading-text, seeders, enhance-enforcementreviewapprovemodal


<!-- Generated by dev-tracker publish_to_jekyll.py (AI mode) -->
<!-- accomplished-date: 2026-05-09 -->
<!-- unit-ids: rd100-stabilize-inherited-working-tree,migration-guard-audit-script,tier-a-cohort-2,tier-a-cohort-3,tier-a-cohort-1,ci-fresh-db-job,cohort-1-webhook-payment-jobs,phpstan-migration-guard-rule,tenant-context-phpstan-rule,job-tenant-context-integration-test,cohort-2-email-notification-jobs,edge-cases-classification,tier-b-column-guards,job-audit-script,cohort-3-etl-sync-jobs,container-seeder-databaseseeder-registration,migration-guard-adr,tenant-context-job-adr,container-seeder-inventory,container-seeder-move,container-seeder-phpstan-rule,fresh-db-clean-run-evidence,tenant-context-allowlist,cohort-4-remaining-jobs,container-seeder-adr,tier-c-resolution,architecture-doc-update,tenant-context-architecture-doc,cti-test-surface-audit,model-scope-isolation-test,role-permission-model-type-mismatch-test,admin-scoped-bypass-policy-test,job-tenant-isolation-test,api-endpoint-tenant-isolation-test,storage-tenant-isolation-test,phpunit-integration-suite-wiring,cross-tenant-canary-workflow,testing-doc-update,rd0-establish-react-doctor-config,rd0-add-fetch-test-support,rd0-land-bounded-baseline-remediation,rd0-extract-focus-trap-utilities,rd0-polish-debug-identifiers-and-story-parity,rd0-integrate-baseline-branch,rd0-commit-current-branch-remediation-wave,rd0-move-open-goal-to-followup-sprint,structured-logging-cross-link,structured-logging-grafana-parse,structured-logging-emitter-grep,structured-logging-coverage-map,structured-logging-dead-panel-resolution,react-doctor-checkpoint-remediation-wave,tenant-aware-tenant-aware-job-documentation-phpstan-rules,loading-text-loading-text-use-ellipsis-marketing,seeders-improve-limit-configuration-handling-tests,enhance-enforcementreviewapprovemodal-enhance-enforcementreviewapprovemodal-with-accessibility-tests -->

<!-- accomplished-unit-ids: admin-scoped-bypass-policy-test,api-endpoint-tenant-isolation-test,architecture-doc-update,ci-fresh-db-job,cohort-1-webhook-payment-jobs,cohort-2-email-notification-jobs,cohort-3-etl-sync-jobs,cohort-4-remaining-jobs,container-seeder-adr,container-seeder-databaseseeder-registration,container-seeder-inventory,container-seeder-move,container-seeder-phpstan-rule,cross-tenant-canary-workflow,cti-test-surface-audit,edge-cases-classification,enhance-enforcementreviewapprovemodal-enhance-enforcementreviewapprovemodal-with-accessibility-tests,fresh-db-clean-run-evidence,job-audit-script,job-tenant-context-integration-test,job-tenant-isolation-test,loading-text-loading-text-use-ellipsis-marketing,migration-guard-adr,migration-guard-audit-script,model-scope-isolation-test,phpstan-migration-guard-rule,phpunit-integration-suite-wiring,rd0-add-fetch-test-support,rd0-commit-current-branch-remediation-wave,rd0-establish-react-doctor-config,rd0-extract-focus-trap-utilities,rd0-integrate-baseline-branch,rd0-land-bounded-baseline-remediation,rd0-move-open-goal-to-followup-sprint,rd0-polish-debug-identifiers-and-story-parity,rd100-stabilize-inherited-working-tree,react-doctor-checkpoint-remediation-wave,role-permission-model-type-mismatch-test,seeders-improve-limit-configuration-handling-tests,storage-tenant-isolation-test,structured-logging-coverage-map,structured-logging-cross-link,structured-logging-dead-panel-resolution,structured-logging-emitter-grep,structured-logging-grafana-parse,tenant-aware-tenant-aware-job-documentation-phpstan-rules,tenant-context-allowlist,tenant-context-architecture-doc,tenant-context-job-adr,tenant-context-phpstan-rule,testing-doc-update,tier-a-cohort-1,tier-a-cohort-2,tier-a-cohort-3,tier-b-column-guards,tier-c-resolution -->
<!-- SECTION: ACCOMPLISHED END -->
<!-- Generated by dev-tracker build_today_plan.py -->
