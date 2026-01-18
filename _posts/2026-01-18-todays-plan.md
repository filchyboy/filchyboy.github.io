---
layout: post
title: "Daily Plan - 2026-01-18"
date: 2026-01-18
---

# Daily Plan - Sunday, January 18, 2026

## Today's Theme
I'm riding the wave of my internationalization momentum - 108 commits this week shows where my strategic focus has been. I last touched this work 3 days ago, so the context is still reasonably fresh. I've got 8 unit test tasks all sitting at the same priority score, which tells me it's time to just pick them up and knock them out systematically. Today is about finishing what I started and clearing these i18n tests off my board.

## The Main Work

**Complete locale resolution testing (i18n-p7-unit-locale-resolution-2 & i18n-p7-unit-locale-resolution-3)**
These are part of the massive i18n feature set I've been building - 108 commits this week speaks to how much energy I've invested here. I need to test both Accept-Language header handling and user preference resolution. These are foundational pieces that everything else depends on, so getting them solid makes sense before I move further into the formatting tests.

**Build out currency formatting tests (i18n-p7-unit-currency-1 & i18n-p7-unit-currency-2)**
Still in that same feature set where I've got strong momentum. Testing USD and EUR formatting separately gives me good coverage of the currency handling system. Since I've been deep in this internationalization work, the mental model of how the currency system should behave is fresh in my head. These should flow naturally.

**Add number formatting tests (i18n-p7-unit-number-1 & i18n-p7-unit-number-2)**
Another pair from my active i18n work - testing thousands separators and decimal handling. These complement the currency tests and round out the numeric formatting coverage. With 108 commits invested in this feature set, I can see the finish line for the core testing suite, and these are part of getting there.

**Implement date formatting test (i18n-p7-unit-date-1)**
One more from the i18n suite - testing short date format. This is part of the same logical grouping as the currency and number tests. Since I'm already in that headspace and have momentum on this feature set, it makes sense to keep pushing through these test tasks while the context is loaded.

## Housekeeping

**Fix that one ESLint error in colorUtils.ts**
This is the only ESLint error I have in the entire codebase right now - 1 error total. That's actually pretty clean, so knocking this out would get me to a fully passing ESLint run. It's in colorUtils.ts, so it's probably something straightforward.

**Review the Blade A11y compliance status**
I'm at 57% compliance with 3,092 violations - mostly inputWithoutId (1,792) and clickWithoutKeyboard (1,288) issues. I don't need to fix all of these today, but I should at least scan through a few of the files to understand the patterns. Maybe I can spot some quick patterns to address in commonly-used components.

## Parked

I've got a huge planning pipeline - 26 different feature sets that need either research or implementation plans. I'm deliberately not touching any of those today because my behavioral signals are crystal clear: I'm deep in internationalization work with massive momentum (108 commits this week). Context-switching to planning work would kill that momentum. Those planning directories will still be there tomorrow.

The 1,696 PHPStan errors are also staying parked. That's a bigger systemic issue that needs focused attention, not something to squeeze into a day where I'm trying to finish my i18n testing suite. I can see there's a phpstan-work planning directory that already has artifacts, so when I'm ready to tackle that, I'll have a place to start.

---

## Update - 10:15 AM

Had a really productive morning building out two major pieces of infrastructure. First, I tackled the context-aware batch testing system that's been on my list for weeks. Started with the foundational scripts - test discovery, the fixed-batch runner, and report merging - then worked through robustness improvements and linter fixes. The interesting part came when I added the --seed option for reproducible test shuffling, which led me down the path of implementing "smart mode." This tracks which tests have been affected by git changes and only runs those, backed by a test ledger system. Changed the default batch size from 75 down to 15 based on some performance observations, and wrapped it all up with proper documentation and Makefile targets.

The second focus was adding PKCE support to my Microsoft OAuth implementation. This one felt more straightforward - created the helper trait for generating code challenges and verifiers, then integrated it into the redirect and callback flows. The OAuth controller needed some refactoring to handle the PKCE validation properly, but the real time went into comprehensive testing. Built unit tests for the helper trait, expanded the controller tests to cover the PKCE scenarios, and finished with an end-to-end feature test that validates the entire flow. It's one of those security improvements that doesn't change the user experience but makes the whole system more robust.

## The Numbers
- Additional tasks: 20
- Feature areas: context-aware-batch-testing, add-pkce

---

## Update - 12:18 PM

I spent the morning building out the formatting utilities that make internationalization actually work in practice. Started with the core ones - currency, date, time, and number formatting - then added relative time formatting since that's something users see everywhere. The real test was making sure these work across all 5 locales I'm supporting, especially with things like Eastern Arabic numerals that can trip up number formatting if you're not careful.

The Typography component got some love too - added the i18n props it needed (key, namespace, and interpolation options) so it can handle translations cleanly. Then I tackled the error pages, creating the errors namespace and translating all the standard HTTP error pages. Testing these in RTL mode was particularly important since error pages are often the first thing users see when something goes wrong. Wrapped up by writing proper unit tests for all the formatting utilities and updating the Storybook stories with i18n examples - the kind of documentation work that pays off when you're debugging locale issues later.

## The Numbers
- Additional tasks: 19
- Feature areas: internationalization
<!-- Generated by dev-tracker publish_to_jekyll.py (AI mode) -->
<!-- accomplished-date: 2026-01-18 -->
<!-- unit-ids: i18n-p2-util-format-currency,i18n-p2-util-format-date,i18n-p2-util-format-time,i18n-p2-util-format-number,i18n-p2-typography-i18n-key,i18n-p2-typography-namespace,i18n-p2-typography-options,i18n-p2-util-format-relative-time,i18n-p2-errors-json-creation,i18n-p2-errors-404,i18n-p2-errors-403,i18n-p2-errors-500,i18n-p2-errors-503,i18n-p2-util-currency-all-locales,i18n-p2-typography-variants-test,i18n-p2-util-tests,i18n-p2-util-arabic-numerals,i18n-p2-typography-storybook,i18n-p2-errors-rtl-test -->

<!-- unit-ids: add-pkce-add-pkce-challenge-to-redirect,add-pkce-controller-pkce-unit-tests,add-pkce-create-pkce-helper-trait,add-pkce-integration-pkce-flow-test,add-pkce-normalize-controller-todo-format,add-pkce-pkce-helper-unit-tests,add-pkce-verify-code-verifier-on-callback,batch-size-change,batch-testing-discovery,batch-testing-docs,batch-testing-linter,batch-testing-merge,batch-testing-robustness,batch-testing-runner,batch-testing-seed,i18n-p2-errors-403,i18n-p2-errors-404,i18n-p2-errors-500,i18n-p2-errors-503,i18n-p2-errors-json-creation,i18n-p2-errors-rtl-test,i18n-p2-typography-i18n-key,i18n-p2-typography-namespace,i18n-p2-typography-options,i18n-p2-typography-storybook,i18n-p2-typography-variants-test,i18n-p2-util-arabic-numerals,i18n-p2-util-currency-all-locales,i18n-p2-util-format-currency,i18n-p2-util-format-date,i18n-p2-util-format-number,i18n-p2-util-format-relative-time,i18n-p2-util-format-time,i18n-p2-util-tests,smart-mode-changes,smart-mode-docs,smart-mode-integration,smart-mode-ledger,smart-mode-makefile -->