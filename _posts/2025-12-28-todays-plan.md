---
layout: post
title: "Daily Plan - 2025-12-28"
date: 2025-12-28
---

# Daily Plan - Sunday, December 28, 2025

## Today's Theme
I touched a lot of different feature sets today during my planning session, and now I need to focus that energy. The behavioral signals are screaming at me to finish the ETL scheduler work - I've got fresh context loaded and high momentum (score of 22-23 across all three tasks). I also want to knock out that scope violation test for MCP Toon since I'm already in that headspace.

## The Main Work

**1. Complete the MCP Toon scope violation test**
I literally touched this today and it's sitting in my "In Progress" column. The context is completely fresh in my head - I know exactly what needs to be tested here. This is about ensuring the MCPToonGuard properly rejects requests that violate scope boundaries. Getting this done clears my only in-progress item and gives me a clean slate.

**2. Build out the ETL scheduler registration flow**
This feature set has my highest behavioral scores (22-23 across the board) because I touched it today and have strong momentum (3.0 momentum score). I need to create the GetScheduleConfigurationsTask, then the RegisterETLSchedulesAction, and finally update Kernel.php to wire it all together. The recency boost (+5.0) means I have the architecture fresh in my mind - I was just thinking through how this needs to work. This re-enables automatic ETL syncing, which is critical infrastructure.

**3. Wire up the daily alert frequency reset job**
Another feature set I touched today with high scores (22-23). I need to create the ResetDailyAlertFrequencyJob class structure and register it in Kernel.php. This is related to the scheduler work above, so doing them together makes sense while I'm in that "scheduled jobs and Kernel registration" headspace. The alert system needs this to function correctly - without it, daily frequency counters just accumulate forever.

**4. Harden the APP_DEBUG default configuration**
Small but important security task that's scored at 23.0 because I touched it today. I need to update the APP_DEBUG default in the .env.example and add a security warning comment. This is literally one file, but it's about preventing production security issues. Since I've got the context loaded from today's planning, I should just knock it out.

## Housekeeping

**Update SsoLogoutButton to use centralized error handling**
This scored 22.0 and I touched it today, so the context is there. It's about migrating the SsoLogoutButton component to use the useAuthError hook for consistent toast UX. This is a good break between the Laravel scheduler work - switching between backend and frontend helps keep my mind fresh.

**Run the existing policy tests after yesterday's refactoring**
I touched the refactor-getpolicyname work today (score: 22.0), and before I go further, I need to validate that my changes didn't break anything. Running the test suite is basic due diligence, and it'll tell me if I need to adjust course on that refactoring work.

## Parked

I'm deliberately setting aside the `run-policy-tests` as a stretch goal rather than core work - if the main ETL and MCP tasks take longer than expected, I can push that verification to tomorrow. The PHPStan issues (2,225 errors) and Jest failures (93 failed tests) are calling to me from the quality reports, but those represent deeper rabbit holes that would derail my momentum on the scheduler and MCP work. The accessibility score of 30% is painful to look at, but that's a multi-day effort that needs dedicated focus, not Sunday afternoon attention.

The planning pipeline items in "Needs Research" and "Needs Implementation Plan" are important future work, but today is about execution on what I've already got context for. I've built the momentum - now I need to ship.