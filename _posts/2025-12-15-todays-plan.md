---
layout: post
title: "Daily Plan - 2025-12-15"
date: 2025-12-15
---

# Daily Plan - Monday, December 15, 2025

## Today's Theme
I'm wrapping up the DSR security work that's been in flight and then pivoting to some foundation layer improvements that keep bubbling up. The configuration system needs some love, and I want to knock out a few quality issues that have been staring at me from the reports.

## The Main Work

**Finish the DSR verification email flow** - I've got two tasks in progress here: the `SendVerificationEmailAction` and the `SubmitDSRRequest` form request. I'm close on both, and I want to close them out before they go stale in my head. Once these are done, I can verify the Phase 7 acceptance criteria and actually call this feature complete.

**Add those configuration helpers** - The `getBoolean` and `getTenantAware` helpers keep coming up as I work through features. I'm tired of writing the same logic over and over, so I'm going to properly add these to the foundation layer. This is one of those things that will make my life easier immediately.

**Create the SystemSettingPolicy** - I need RBAC on the configuration system. It's been bothering me that there's no proper policy in place, and with the helpers going in, now's the right time to add the policy layer. This is a 3-effort task but it's foundational work that unblocks future configuration features.

## Housekeeping

**Tackle FluentCrmAdapter PHPStan errors** - This file is sitting at 37 errors and it's the top offender in the PHPStan report. I should carve out some time to work through at least a portion of these. Even getting it down to 20 errors would feel like progress.

**Review the test-refactor planning directory** - The research is done and it explicitly calls out that ADR-0001 and the PHPUnit structure docs require container-scoped test directories. I should spend some time creating an implementation plan so this doesn't just sit in "needs implementation plan" limbo forever.

## Parked

Nothing's technically blocked right now, but I'm deliberately setting aside the Groundhogg idempotency work and the accessibility report generation. Both are important, but the DSR security finish line is more urgent, and I want to get those foundation helpers in place before I context-switch to integration patterns or accessibility work.