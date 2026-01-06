---
layout: post
title: "Daily Plan - 2026-01-06"
date: 2026-01-06
---

# Daily Plan - Tuesday, January 06, 2026

## Today's Theme

I'm riding the momentum on internationalization - I was just in that code yesterday and the feature set is showing high activity (3.0 momentum score). With 8 ready-to-start tasks all scoring 23.0, I want to knock out a solid chunk of these translation tasks while the context is fresh in my head. This is strategic work that'll pay dividends for our global users, and I've got the mental model loaded up from yesterday's work.

## The Main Work

**1. Translate invoice header, line items, and totals (i18n-p5-invoice-header, i18n-p5-invoice-line-items, i18n-p5-invoice-totals)**

I'm grouping these three together because they're all part of the invoice UI and it makes sense to tackle them as a cohesive unit. I was working on the internationalization feature set yesterday (recency: +5.0), so I've got fresh context on our i18n patterns. The invoice is a critical user-facing component where poor translation would be really noticeable, so getting these done properly matters. I'll work through the header first, then line items, then the totals section - following the natural flow of how users read an invoice.

**2. Translate credit card form labels (i18n-p5-payment-card-labels)**

This is another high-visibility component where translation quality matters. Since I'll already be in the payment/billing UI space after doing the invoices, the context switch is minimal. Payment forms are sensitive - users need to trust them - so having proper localization here isn't just nice-to-have, it's essential for international conversions. Same recency and momentum signals as the invoice work (+5.0 recency, +3.0 momentum).

**3. Add interpolation variable check to CI/CD (i18n-p6-cicd-interpolation-check)**

This is preventative infrastructure work that'll save me from translation bugs down the road. Since I'm actively working on translations today, I'm acutely aware of how easy it is to mess up interpolation variables (like missing a `{variable}` in a translation string). Adding this check to CI/CD means I'll catch these mistakes automatically before they hit production. It's the right time to do this while I'm thinking about i18n quality.

**4. Test locale resolution: route prefix (i18n-p7-unit-locale-resolution-1)**

I want to get at least one of the locale resolution tests done today to start validating the core routing behavior. Route prefix detection is the most common way users will switch languages, so it's the logical first test to write. This is still riding the same i18n momentum, and having test coverage will give me confidence as I continue building out the translation work in future sessions.

## Housekeeping

**Review PHPStan errors in coppa.php (22 errors)**

The COPPA compliance file is at the top of my PHPStan error list with 22 errors. That's a lot for a single file, and given that COPPA is compliance-related work, I should make sure the types are solid there. I'll spend 30-45 minutes working through what I can fix easily - this might be mostly type hints and docblock improvements.

**Check the Blade A11y violations for inputWithoutId issues**

With 1,792 instances of inputs without IDs, this is clearly a systemic pattern I need to understand. I won't fix all of them today, but I should look at a few examples to understand the root cause. Are these coming from a common component? Is this a pattern I'm repeating? Understanding it now will help me avoid creating more of these issues in the i18n forms I'm working on today.

## Parked

I'm deliberately setting aside the other four i18n test tasks (locale resolution via Accept-Language header and user preference) for now. I want to see how the first test goes before committing to all three test scenarios today. If the route prefix test reveals complexity I'm not expecting, I'll adjust tomorrow's plan accordingly.

No blocked work to worry about, which is nice - I've got clear runway on everything I'm tackling today.

---

## Update - 11:00 AM

Made serious headway on the internationalization foundation today. Started by getting the basic infrastructure in place - installed the frontend i18n dependencies and ran the database migrations to create the locale tables. Then I built out the core backend services: LocaleResolutionService to handle language detection, SetLocaleMiddleware to apply it across requests, and a pair of actions for getting and setting user locale preferences. The API endpoint for serving translations came together smoothly, and I got the middleware properly registered in the kernel.

The frontend setup required more orchestration - created the i18n configuration files, set up the I18nextProvider integration in App.tsx, and built out the LocaleContext for state management. Added support for locale route prefixes and created a FormatCurrencyTask for handling monetary displays across different regions. The translation files themselves were a bit of a grind - started with English (common, auth, navigation, forms, billing, admin), then created the full sets for Spanish, French, Arabic, and Hebrew. Getting the directory structure right and ensuring consistency across all the language files took longer than expected, but now I have a solid foundation for the multi-language rollout.

## The Numbers
- Additional tasks: 28
- Feature areas: internationalization

---

## Update - 12:10 PM

Made solid progress on the CDP identity resolution system today. I spent most of the morning building out the logging infrastructure - created the IdentityResolutionLog model, wired up the population logic in ResolveIdentityAction, and got the tests in place. It's one of those foundational pieces that isn't glamorous but makes debugging so much easier down the road. Also added a factory for it, which will help with testing scenarios.

The afternoon was all about making the identity matching more configurable and robust. I externalized the nickname dictionary to JSON config (no more hardcoded arrays), added diacritics removal to the NameSimilarityService, and made the deterministic rule order configurable. The cursor tracking system came together nicely too - built the migration, service, and model, then integrated it into the CRM adapters. Between that work, I knocked out documentation for four more containers (Telemetry, Tenancy, Regulatory, and Theme) and added comprehensive unit tests for all 14 WooCommerce Pull/Push tasks. The CDP work feels like it's reaching a more mature state with all this configuration flexibility and logging in place.

## The Numbers
- Additional tasks: 22
- Feature areas: cdp-deep-dive, container-docs, woocommerce
<!-- Generated by dev-tracker publish_to_jekyll.py (AI mode) -->
<!-- accomplished-date: 2026-01-06 -->
<!-- unit-ids: cdp-p2-log-model,cdp-p2-log-population,cdp-p2-log-tests,container-docs-document-core-telemetry,container-docs-document-core-tenancy,container-docs-document-core-regulatory,cdp-p2-log-factory,cdp-p2-config-version-tracking,cdp-p2-diacritics-removal,container-docs-document-core-theme,cdp-p2-config-version-tests,cdp-p2-diacritics-tests,woocommerce-add-unit-tests-for-all-14-pullpush-tasks,cdp-p2-nickname-externalize,cdp-p2-rule-order-config,cdp-p2-cursor-migration,cdp-p2-nickname-tests-update,cdp-p2-rule-order-tests,cdp-p2-cursor-service,cdp-p2-cursor-integration,cdp-p2-cursor-model,cdp-p2-cursor-tests -->

<!-- unit-ids: cdp-p2-config-version-tests,cdp-p2-config-version-tracking,cdp-p2-cursor-integration,cdp-p2-cursor-migration,cdp-p2-cursor-model,cdp-p2-cursor-service,cdp-p2-cursor-tests,cdp-p2-diacritics-removal,cdp-p2-diacritics-tests,cdp-p2-log-factory,cdp-p2-log-model,cdp-p2-log-population,cdp-p2-log-tests,cdp-p2-nickname-externalize,cdp-p2-nickname-tests-update,cdp-p2-rule-order-config,cdp-p2-rule-order-tests,container-docs-document-core-regulatory,container-docs-document-core-telemetry,container-docs-document-core-tenancy,container-docs-document-core-theme,i18n-p1-action-get-tenant-locales,i18n-p1-action-get-user-locale,i18n-p1-action-set-user-locale,i18n-p1-api-translations-endpoint,i18n-p1-db-run-migrations,i18n-p1-fe-config-ts,i18n-p1-fe-i18n-ts,i18n-p1-fe-install-deps,i18n-p1-fe-locale-context,i18n-p1-fe-provider-integration,i18n-p1-fe-types-ts,i18n-p1-json-ar-all,i18n-p1-json-en-admin,i18n-p1-json-en-auth,i18n-p1-json-en-billing,i18n-p1-json-en-common,i18n-p1-json-en-forms,i18n-p1-json-en-navigation,i18n-p1-json-es-all,i18n-p1-json-fr-all,i18n-p1-json-he-all,i18n-p1-locales-dir-structure,i18n-p1-middleware-register,i18n-p1-middleware-set-locale,i18n-p1-routes-locale-prefix,i18n-p1-service-locale-resolution,i18n-p1-task-format-currency,i18n-p1-task-get-translation-provider,woocommerce-add-unit-tests-for-all-14-pullpush-tasks -->