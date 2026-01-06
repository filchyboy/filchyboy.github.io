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