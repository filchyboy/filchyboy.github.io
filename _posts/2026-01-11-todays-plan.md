---
layout: post
title: "Daily Plan - 2026-01-11"
date: 2026-01-11
---

# Daily Plan - Sunday, January 11, 2026

## Today's Theme
I'm laser-focused on wrapping up the internationalization feature set today. I've been absolutely heads-down on this work—94 commits this week—and touched it just 2 days ago, so the context is still fresh in my head. All 8 remaining tasks have identical high scores (22.0), which tells me they're all equally ready to knock out. I want to maintain this momentum and clear as many of these translation tasks as possible before the week starts.

## The Main Work

**1. Translate invoice header (i18n-p5-invoice-header)**
This is part of the internationalization feature set where I've invested heavily this week (94 commits). I worked on related translation tasks 2 days ago, so I still have the invoice structure fresh in my mind. The invoice header is the first thing users see on billing documents, so getting this translated properly sets the foundation for the remaining invoice components.

**2. Translate invoice line items (i18n-p5-invoice-line-items)**
Following directly from the header work, this makes sense as the next piece. I've been in the invoice translation flow, and tackling line items while I'm already in that context keeps me from context-switching. The behavioral signals show this has the same priority score as the header (22.0), and doing these sequentially will let me verify the complete invoice rendering in one go.

**3. Translate invoice subtotal/tax/total (i18n-p5-invoice-totals)**
Completing the invoice totals finishes the entire invoice translation suite. Since I'll already have the header and line items done, wrapping up the totals section gives me a complete, testable feature I can demo. This is part of the same high-momentum feature set (94 commits this week), and finishing the full invoice flow feels like a meaningful milestone.

**4. Translate credit card form labels (i18n-p5-payment-card-labels)**
The payment forms are closely related to the invoice work—they're both part of the billing experience. I've been working in this problem space recently (2 days ago), so the payment flow context is still loaded in my head. Knocking this out while I'm already thinking about billing and payments is more efficient than coming back to it later.

**5. Add interpolation variable check to CI/CD (i18n-p6-cicd-interpolation-check)**
This is a quality gate I need to establish before I get too deep into more translation work. I've already translated a bunch of strings this week (94 commits worth), and adding this check now will catch any interpolation mistakes in all the work I've done so far. It's preventative maintenance that pays dividends immediately, and it keeps the i18n momentum going while shifting to infrastructure for a bit of variety.

## Housekeeping

**Fix the ESLint error in colorUtils.ts**
There's exactly 1 ESLint error in the entire codebase right now, and it's in colorUtils.ts. That's too clean a slate to ignore—I should just fix it and get back to a fully green linter. It'll take a few minutes and keeps the codebase health high.

**Review the PHPStan top offenders list**
With 8,411 errors, I'm not going to fix PHPStan today, but I should at least look at why MultiCurrencyDashboardTestDataEmitterTest.php has 57 errors and LoggingKpiTestDataEmitterTest.php has 52. Understanding the pattern might inform how I approach future test writing, especially if these are related to the i18n work I'm doing.

## Parked

I'm deliberately setting aside the locale resolution unit tests (i18n-p7-unit-locale-resolution-1, -2, -3) today. They're part of the same high-priority i18n feature set, but I want to focus on user-facing translations first. The route prefix, Accept-Language header, and user preference tests are important, but they're verification work that can wait until I have more of the actual translation strings in place. Better to have translated content to test with than perfect tests for incomplete translations.

The planning pipeline has a lot of items needing implementation plans, but I'm not going to derail my i18n momentum to do planning work today. That's better suited for a weekday when I might have less flow time for deep feature work.