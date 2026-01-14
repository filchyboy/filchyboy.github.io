---
layout: post
title: "Daily Plan - 2026-01-14"
date: 2026-01-14
---

# Daily Plan - Wednesday, January 14, 2026

## Today's Theme
I'm laser-focused on the internationalization feature set today. I was just working on this yesterday (⚡ recently active), and I've built up serious momentum with high commit frequency this week. I've got 8 unit tests ready to start, all with identical priority scores (23.0), so it makes sense to batch through these while the context is hot in my head. This is the kind of day where I can make real progress on a focused feature set.

## The Main Work

**1. Complete locale resolution tests (i18n-p7-unit-locale-resolution-2 and i18n-p7-unit-locale-resolution-3)**

I'm starting here because I touched this feature set just yesterday (+5.0 recency score), and I've been investing heavily in internationalization work this week (+3.0 momentum). The context around locale resolution is fresh in my mind - how the Accept-Language header parsing works, how user preferences override defaults. I'll knock out both the header-based resolution test and the user preference test since they're related and I can batch the setup work.

**2. Build out currency formatting tests (i18n-p7-unit-currency-1 and i18n-p7-unit-currency-2)**

Still riding the i18n momentum here. Currency formatting is critical for a SaaS platform - USD and EUR are our two most common currencies, so these tests need to be solid. Since I'm already deep in the internationalization context from working on locale resolution, it makes sense to keep going rather than context-switching. The behavioral signals are clear: recency +5.0, momentum +3.0 - I'm in the zone on this feature set.

**3. Implement number and date formatting tests (i18n-p7-unit-number-1, i18n-p7-unit-number-2, i18n-p7-unit-date-1)**

Rounding out the formatting layer of the i18n work. Number formatting (thousands separators, decimal precision) and date formatting (short format) are the last pieces of the formatting test suite. All three tasks have the same priority score (23.0) and they're closely related - I can set up similar test fixtures and assertion patterns. This completes a logical chunk of the internationalization work and gets me closer to shipping this feature set.

**4. Test JsonFileProvider loading (i18n-p7-unit-provider-1)**

This is the foundation test for how we load translation files. Even though it's got the same score as the others (23.0), I'm putting it last because it's slightly different from the formatting tests - it's more about the infrastructure layer. But I need to get it done while I'm still in the i18n headspace. Once I complete this, I'll have knocked out all 8 of the ready-to-start internationalization tasks.

## Housekeeping

**Fix the ESLint error in colorUtils.ts**

There's literally one ESLint error in the entire codebase, and it's in colorUtils.ts. That's too clean to ignore - I'll spend a few minutes fixing it between i18n tasks. It's probably something trivial, and getting ESLint to 100% clean feels good.

**Review PHPStan errors in MergeSuggestionTest.php**

The PHPStan report shows 23 errors in this one test file - that's the highest count in the codebase. I'm not going to fix all 1,832 PHPStan errors today, but spot-checking the top offender might reveal a pattern I can address quickly or at least understand better for future cleanup work.

## Parked

I'm deliberately not touching any of the planning pipeline items today, even though there are a bunch of directories that need research or implementation plans. The internationalization work has clear momentum (yesterday's activity, this week's commits), and I need to ride that wave while the context is loaded. Planning work requires a different headspace - I'll save that for a day when I'm not deep in implementation mode.

The blocked list is empty, which is great - nothing's waiting on external dependencies. I'm also setting aside the Blade accessibility violations (3,092 issues) for now. That's a bigger project that needs dedicated focus, not something to squeeze in around i18n work.