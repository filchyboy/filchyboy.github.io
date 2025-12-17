---
layout: post
title: "Daily Plan - 2025-12-17"
date: 2025-12-17
---

# Daily Plan - Wednesday, December 17, 2025

## Today's Theme
I'm focusing on foundational infrastructure improvements today. The accessibility report task is small enough to knock out first thing, then I want to tackle those helper methods that will make configuration management cleaner across the platform. If I have energy left, I'll start hardening the Groundhogg idempotency work.

## The Main Work

**Generate accessibility report for location views** - I'll start here because it's focused and will give me a quick win to build momentum. My accessibility score is at 30% which is honestly embarrassing, and I need to start getting visibility into where the problems are. This report will help me understand what's broken in the location views specifically.

**Add getBoolean/getTenantAware helpers to configuration** - This is foundation work that's been nagging at me. Right now I'm probably doing config lookups inconsistently across the codebase, and having proper helpers will make tenant-aware configuration much cleaner. This is the kind of refactor that pays dividends every time I touch config code going forward.

**Implement reserve/release pattern in batchSync transform loop** - The Groundhogg idempotency work needs this pattern to prevent race conditions during batch syncing. It's a 3-effort task so it'll take some concentration, but getting the reserve/release pattern right now means the unit tests (next task in that feature set) will be much more straightforward to write. I want to at least make solid progress on this today.

## Housekeeping

**PHPStan cleanup in AdminLoginController.php** - I've only got 8 PHPStan errors total, which is pretty good. I should knock out the AdminLoginController error since authentication code needs to be rock solid. Quick fix that keeps my static analysis green.

**Review the test-refactor planning directory** - It has research done and mentions that my ADR-0001 and PHPUnit structure docs require container-scoped test directories. I need to create an implementation plan for this because my PHP test pass rate at 72% is pretty terrible. I should spend 20 minutes outlining what needs to happen here so it's ready to execute soon.

## Parked

Nothing's explicitly blocked right now, which is good. I'm deliberately not touching the RTK upgrade CSS properties work or the resilience rollout tasks today - those can wait until tomorrow. The Groundhogg idempotency tests are also going to wait until I get the reserve/release pattern working properly.