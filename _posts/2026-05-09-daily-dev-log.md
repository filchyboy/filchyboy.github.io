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
<!-- accomplished-generated: 2026-05-09T18:57:09.787248+00:00 -->

## Today's Update

Today turned into one of those days where several architectural threads finally came together into something coherent. I completed two major cross-container boundary implementations - the MCP-TrustFabric event system and a comprehensive tenant-aware job enforcement system - plus made significant progress on both the React Doctor remediation work and structured logging cleanup.

The MCP-TrustFabric boundary work was the most satisfying piece. I built out a complete event-driven communication system between these two containers, replacing the messy direct imports that had been bothering me for weeks. The flow is clean now: MCP dispatches PolicyDecisionRequested events, TrustFabric listens and processes them through its policy engine, then fires back PolicyDecisionRecorded events with the results. I added a custom PHPStan rule called BanCrossContainerImportRule to prevent future violations, complete with an allowlist for the few shared types that are genuinely unavoidable. The integration test proved the whole cycle works end-to-end, and I documented the approach in an ADR since this pattern will probably get reused elsewhere.

The tenant-aware job work followed a similar pattern but touched way more of the codebase. I audited all our queued job classes for tenant context issues, then systematically converted them in four cohorts: webhook handlers and payment jobs first, then email and notifications, ETL and sync jobs, and finally the remaining stragglers. Each job class now properly propagates tenant context through the queue system, which should eliminate the data leakage bugs we've been seeing in multi-tenant scenarios. Added another PHPStan rule - RequireTenantAwareJobRule - to enforce this going forward, plus integration tests that verify jobs stay isolated to their tenant boundaries.

I also pushed through two waves of React Doctor remediation work. The baseline remediation involved setting up the repo-level config, building out shared fetch mock utilities, and applying fixes across a targeted set of components. The follow-up wave addressed the inherited remediation batch that had been sitting in an unstable state. Both waves included focus-trap utilities for the modal components and improved debug identifiers for testing. I'm still short of the 100/100 target I was aiming for, but the remediation infrastructure is solid now and the remaining fixes should go faster.

The structured logging work wrapped up some loose ends from previous sprints. I cross-linked with the next-wave effort, parsed our Grafana dashboard JSON to identify which log keys are actually being used, and produced a coverage map that revealed several dead dashboard panels. Not glamorous, but this kind of maintenance prevents the monitoring system from becoming a graveyard of broken charts.

This architectural cleanup work should pay dividends over the next few weeks - cleaner boundaries, better tenant isolation, and more reliable frontend testing infrastructure.


<!-- Generated by dev-tracker publish_to_jekyll.py (AI mode) -->
<!-- accomplished-date: 2026-05-09 -->
<!-- unit-ids: rd100-stabilize-inherited-working-tree,policy-decision-requested-event,policy-decision-recorded-event,mcp-policy-decision-dispatch,trustfabric-policy-decision-listener,trustfabric-policy-decision-recorded-dispatch,ban-cross-container-import-rule,ban-cross-container-import-allowlist,policy-decision-event-integration-test,mcp-tf-event-boundary-adr,mcp-tf-cutover-remove-direct-import,job-audit-script,cohort-1-webhook-payment-jobs,cohort-2-email-notification-jobs,cohort-3-etl-sync-jobs,cohort-4-remaining-jobs,tenant-context-phpstan-rule,tenant-context-allowlist,job-tenant-context-integration-test,tenant-context-job-adr,tenant-context-architecture-doc,rd0-establish-react-doctor-config,rd0-add-fetch-test-support,rd0-land-bounded-baseline-remediation,rd0-extract-focus-trap-utilities,rd0-polish-debug-identifiers-and-story-parity,rd0-integrate-baseline-branch,rd0-commit-current-branch-remediation-wave,rd0-move-open-goal-to-followup-sprint,structured-logging-cross-link,structured-logging-grafana-parse,structured-logging-emitter-grep,structured-logging-coverage-map,structured-logging-dead-panel-resolution,react-doctor-checkpoint-remediation-wave,tenant-aware-tenant-aware-job-documentation-phpstan-rules,loading-text-loading-text-use-ellipsis-marketing,seeders-improve-limit-configuration-handling-tests,enhance-enforcementreviewapprovemodal-enhance-enforcementreviewapprovemodal-with-accessibility-tests -->

<!-- accomplished-unit-ids: ban-cross-container-import-allowlist,ban-cross-container-import-rule,cohort-1-webhook-payment-jobs,cohort-2-email-notification-jobs,cohort-3-etl-sync-jobs,cohort-4-remaining-jobs,enhance-enforcementreviewapprovemodal-enhance-enforcementreviewapprovemodal-with-accessibility-tests,job-audit-script,job-tenant-context-integration-test,loading-text-loading-text-use-ellipsis-marketing,mcp-policy-decision-dispatch,mcp-tf-cutover-remove-direct-import,mcp-tf-event-boundary-adr,policy-decision-event-integration-test,policy-decision-recorded-event,policy-decision-requested-event,rd0-add-fetch-test-support,rd0-commit-current-branch-remediation-wave,rd0-establish-react-doctor-config,rd0-extract-focus-trap-utilities,rd0-integrate-baseline-branch,rd0-land-bounded-baseline-remediation,rd0-move-open-goal-to-followup-sprint,rd0-polish-debug-identifiers-and-story-parity,rd100-stabilize-inherited-working-tree,react-doctor-checkpoint-remediation-wave,seeders-improve-limit-configuration-handling-tests,structured-logging-coverage-map,structured-logging-cross-link,structured-logging-dead-panel-resolution,structured-logging-emitter-grep,structured-logging-grafana-parse,tenant-aware-tenant-aware-job-documentation-phpstan-rules,tenant-context-allowlist,tenant-context-architecture-doc,tenant-context-job-adr,tenant-context-phpstan-rule,trustfabric-policy-decision-listener,trustfabric-policy-decision-recorded-dispatch -->
<!-- SECTION: ACCOMPLISHED END -->
<!-- Generated by dev-tracker build_today_plan.py -->
