---
layout: post
title: "Daily Plan - 2026-01-03"
date: 2026-01-03
---

# Daily Plan - Saturday, January 03, 2026

## Today's Theme
I've got fresh momentum on two feature sets today - both internationalization and payment-gateway-controller show recent activity. The i18n work has been getting serious attention (those high scores reflect both recency and momentum), and I want to keep that energy going. I'm thinking I'll knock out the in-progress Form Request work first to clear that mental stack, then ride the i18n wave for the rest of the day.

## The Main Work

**Finish pgc-004-base-form-requests** - I started this yesterday and it's currently in progress. The context is already loaded in my head, and leaving half-finished Form Request work is just going to create friction when I come back to it. Better to close this out and clear it from my active work list.

**i18n-p5-invoice-header** - The internationalization feature set is scoring 23.0 across the board because I touched it today AND I've been committing heavily to it this week. The invoice translation work is part of a clear sequence (header → line items → totals), so starting with the header makes sense. I've got fresh context on the translation patterns and this will flow naturally.

**i18n-p5-invoice-line-items** - Following directly from the invoice header work. These three invoice tasks (header, line items, totals) are clearly meant to be tackled together as a unit. Since I'm already in the invoice translation mindset from the header work, knocking out the line items keeps the momentum without context-switching.

**i18n-p5-invoice-totals** - Completing the invoice translation trilogy. By the end of this, I'll have the entire invoice component fully internationalized, which feels like a meaningful completion point. Better to finish a whole slice of functionality than to leave it 2/3 done.

**i18n-p5-payment-card-labels** - The fourth P5-level i18n task with the same high score (23.0). Since I'll already be deep in translation work from the invoice tasks, adding the credit card form labels is a natural extension. These are all user-facing payment flow elements, so they belong together thematically.

## Housekeeping

**Review PHPStan errors in coppa.php** - This file is the top offender with 22 errors. The COPPA compliance stuff is critical from a regulatory standpoint, and letting type safety issues accumulate there feels risky. I don't need to fix all 22 today, but I should at least understand what's going on.

**Check the failing Jest tests** - 22 tests are failing and the pass rate dropped to 97.8%. That's still pretty good, but I want to make sure these aren't related to the internationalization work I've been doing. If I broke something with recent i18n changes, better to catch it now while the context is fresh.

## Parked

The remaining three i18n tasks (the CI/CD interpolation check and the three unit tests for locale resolution) are all scoring 23.0 as well, but I'm setting them aside for now. Eight i18n items is ambitious enough - if I get through five of them, that's a solid day. The interpolation check and locale resolution tests are more technical/testing-focused, while the invoice and payment label work is user-facing translation. I'd rather complete the user-visible stuff first and save the testing infrastructure for when I have a different kind of energy.