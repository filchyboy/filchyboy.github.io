---
layout: post
title: "Daily Plan - 2026-01-16"
date: 2026-01-16
---

# Daily Plan - Friday, January 16, 2026

## Today's Theme
I'm wrapping up the week with some high-momentum finishes. I've got two items I touched just yesterday that are sitting at the top of my queue, and the internationalization feature set has been absolutely on fire this week with 123 commits. Today feels like a good day to knock out those recently-touched items and then drive forward on the i18n testing work that I've been so deeply invested in.

## The Main Work

**Re-enable the ETL sync scheduler integration**
I worked on this yesterday (recency score +5.0), so the context is completely fresh in my head. The task is straightforward - I need to update Kernel.php to use RegisterETLSchedulesAction. This has strong momentum (+3.0) behind it, and since I was just in this code, I know exactly what needs to happen. Getting the scheduler properly re-enabled will unblock some of the ETL work that's been waiting.

**Migrate SsoLogoutButton to use the centralized toast UX**
Another one from yesterday (recency +5.0), and it's part of cleaning up how I handle SSO logout errors across the platform. The momentum score (+3.0) tells me I've been actively working in this area. Since I already built out the useAuthError hook, migrating this logout button is just about applying the pattern I established. It'll give me consistent error messaging across the SSO flow, which has been bothering me.

**Drive forward on i18n unit testing**
The internationalization feature set has 123 commits this week - that's where my strategic focus has clearly been. I touched this 2 days ago, so the context is still warm. I've got six testing tasks all scored at 22.0, and I want to make meaningful progress on at least 3-4 of them today:
- Locale resolution with Accept-Language headers
- User preference locale resolution  
- USD and EUR currency formatting
- Date and number formatting tests

These are all foundational tests that validate the i18n infrastructure I've been building. Given how much momentum I have here, it makes sense to stay in this zone and build out the test coverage while everything's fresh.

## Housekeeping

**Fix that ESLint error in colorUtils.ts**
There's literally one ESLint error in the entire frontend codebase, and it's in colorUtils.ts. That's been nagging at me - I should just knock it out and get back to a clean slate.

**Start documenting the tailwind-migration implementation plan**
The migration is 39.1% complete, I've got artifacts in place, but I haven't written out a concrete implementation plan yet. I should spend 30 minutes sketching out the next phase so I'm not constantly context-switching when I pick this back up.

## Parked

The rest of the i18n testing suite (the other 2-3 tasks I won't get to today) will roll into next week - they're not going anywhere and the momentum will carry forward. All the planning pipeline items that need research or implementation plans are staying on the backburner for now. I need to stay focused on execution today, not planning. The PHPStan errors (8,606 of them) continue to mock me, but that's a dedicated cleanup effort I'll tackle when I have a clear run at it - not something to weave into a day like today.