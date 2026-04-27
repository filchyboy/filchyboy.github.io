---
layout: post
title: "Daily Dev Log - 2026-04-27"
date: 2026-04-27
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-04-27T14:53:05.376769+00:00 -->

## Today's Theme

The todo-remediation work is pulling me in - I marked it recently active and have 9 units ready to tackle, starting with replacing template boilerplate that's been irritating me. But those PHP tests being 9 days stale is genuinely bothering me because I keep making decisions based on outdated failure data. Plus I'm curious what those 291 untracked commits actually accomplished - that's substantial work that isn't captured anywhere.

## The Main Work

**Replace the template boilerplate in planning directory** - This todo-remediation task has been bugging me because every time I create new planning directories, I'm copying placeholder text that says "TODO: replace this". It's a small thing but it creates visual noise when I'm trying to focus on actual planning content. The boilerplate replacement should be straightforward - just need to audit what template files exist and swap in proper documentation.

**Fix the inventory generator's empty payload.todos[] bug** - The todo tracking system is supposed to populate an array of todo items, but I suspect it's returning empty arrays even when todos exist. This explains why my todo inventory reports have been useless lately. I need to dig into the generator logic and figure out where the array population is failing - probably a simple bug in the scanning regex or file filtering.

**Run those stale PHP test batches** - Nine days old test results are worthless for making architectural decisions. I keep referencing that 88% pass rate but have no idea if recent changes broke anything or fixed flaky tests. Running `make test-fixed-batches-quick` will give me current failure data and maybe reveal if all that infrastructure work from the untracked commits improved our test stability.

**Activate the PHPStan TodoFormatRule** - This rule enforcement will catch malformed todos before they get committed, which prevents the inventory system from missing items due to format inconsistencies. The todo-format-rules.neon file exists but isn't being included in the main PHPStan config. Simple configuration change that should improve todo tracking accuracy going forward.

## Housekeeping

**Regenerate the inventory baseline snapshot** - The artifacts/ directory needs fresh baseline data after all the recent todo format fixes, and this provides clean reference data for future inventory comparisons.

**Extend the inventory generator exclude list** - Add generators, fixtures, and vendor build directories to the exclusion patterns so the inventory focuses on actual application code rather than generated or third-party content.

**Draft implementation plan for review-finding-remediation** - This planning directory aligns with the remediation work I'm already doing, and the quality-gates.md artifact suggests it's about code review process improvements. Good time to advance the planning while remediation concepts are loaded.

## Parked

The 8 remaining todo-remediation units will have to wait - I want to see if fixing the inventory generator and template issues reveals more problems before tackling the frontend reformatting work. The PHPStan file remediation harness with its 9913 units is staying parked until I have better todo tracking infrastructure in place.

<!-- plan-unit-ids: csp-alpine-audit,loc-followup-quick-wins,shopify-webhook-service,sync-routes-health-check,sync-routes-report,todoremed-p0-fix-inventory-empty-todos-bug,todoremed-p0-replace-template-boilerplate -->
<!-- SECTION: DAILY-PLAN END -->


<!-- SECTION: ACCOMPLISHED START -->
<!-- accomplished-generated: 2026-04-27T21:58:03.122354+00:00 -->

## Today's Update

Today I focused heavily on two major refactoring efforts that have been on my mind for weeks - the ShopifyAdapter and the SyncRoutesOverview service. Both had grown into these unwieldy classes that were doing way too much, and I finally had the mental clarity to break them apart properly.

The ShopifyAdapter work was the most substantial. I went through a systematic six-phase refactoring approach, starting with low-risk transformation traits and gradually building up to the complex stuff. Created infrastructure traits for HTTP handling and metrics, then domain-specific traits for webhooks, tombstones, and pagination logic. The entity pull/push traits were probably the trickiest part - lots of interdependent methods that had to be carefully extracted without breaking the existing API contracts. By the time I got to creating the stateless service classes for bulk operations and query building, the adapter was looking much cleaner. Finished by fixing all the PHPStan errors that surfaced during the refactoring - ended up with an 82% reduction in complexity according to the static analysis metrics.

The SyncRoutesOverview service got similar treatment, though it was more straightforward. Extracted the PerformRouteHealthChecksTask and GenerateRouteHealthReportTask as separate, focused classes. The original service now just orchestrates these tasks instead of doing all the work inline. It's one of those changes that seems obvious in hindsight but took forever to actually implement because the coupling was so tight.

I also spent time on some UI improvements around the sidebar navigation - added proper toggle behavior for the admin layout with accessibility enhancements. The NavDrawerToggleTest work revealed some edge cases in how the toggle state was being managed across page refreshes. Not glamorous work, but these kinds of UX polish items really add up over time.

The day wrapped up with a bunch of PHPStan remediation across various migration files - webhook encryption, DSR billing accounts, agents foreign keys, campaigns audience, and email contacts. These were all minor fixes but they were cluttering up the static analysis output. TokenBridgeService also got some attention for streamlining token retrieval and improving error handling, though that was more incremental than the major refactoring work.


<!-- Generated by dev-tracker publish_to_jekyll.py (AI mode) -->
<!-- accomplished-date: 2026-04-27 -->
<!-- unit-ids: sync-routes-orchestration,sync-routes-health-check,sync-routes-report,shopify-refactor-phase1-traits,shopify-refactor-phase2-http,shopify-refactor-phase3-domain,shopify-refactor-phase4-entity,shopify-refactor-phase5-services,shopify-refactor-phase6-phpstan,sidebar-toggle-sidebar-toggle-behavior-admin-layout,enhance-shopifyadapter-refactoring-enhance-shopifyadapter-refactoring-documentation-improve,sync-routes-extract-health-check-report-generation,complete-shopifyadapter-refactoring-complete-shopifyadapter-refactoring-with-traits,enhance-sidebar-navigation-enhance-sidebar-navigation-with-toggle,navdrawertoggletest-navdrawertoggletest-sidebar-toggle-button-accessibility,phpstan-webhook-encrypt-migration-fix,phpstan-dsr-billing-migration-fix,phpstan-agents-fk-migration-fix,phpstan-campaigns-migration-fix,phpstan-email-contacts-drop-migration-fix,enhance-shopifyadapter-enhance-shopifyadapter-with-idempotency-key,streamline-token-retrieval-streamline-token-retrieval-enhance-error -->

<!-- accomplished-unit-ids: complete-shopifyadapter-refactoring-complete-shopifyadapter-refactoring-with-traits,enhance-shopifyadapter-enhance-shopifyadapter-with-idempotency-key,enhance-shopifyadapter-refactoring-enhance-shopifyadapter-refactoring-documentation-improve,enhance-sidebar-navigation-enhance-sidebar-navigation-with-toggle,navdrawertoggletest-navdrawertoggletest-sidebar-toggle-button-accessibility,phpstan-agents-fk-migration-fix,phpstan-campaigns-migration-fix,phpstan-dsr-billing-migration-fix,phpstan-email-contacts-drop-migration-fix,phpstan-webhook-encrypt-migration-fix,shopify-refactor-phase1-traits,shopify-refactor-phase2-http,shopify-refactor-phase3-domain,shopify-refactor-phase4-entity,shopify-refactor-phase5-services,shopify-refactor-phase6-phpstan,sidebar-toggle-sidebar-toggle-behavior-admin-layout,streamline-token-retrieval-streamline-token-retrieval-enhance-error,sync-routes-extract-health-check-report-generation,sync-routes-health-check,sync-routes-orchestration,sync-routes-report -->
<!-- SECTION: ACCOMPLISHED END -->
<!-- Generated by dev-tracker build_today_plan.py -->
