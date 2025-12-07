---
layout: post
title: "Daily Plan - 2025-12-07"
date: 2025-12-07
---

# Daily Plan - Sunday, December 07, 2025

## Today's Theme
I'm building out the core API routes for cross-regional sync today. These are the fundamental endpoints that'll enable my regions to talk to each other and keep data consistent. It's all fresh work, which means I get to establish patterns that'll carry through the rest of this feature set.

## The Main Work

**Create the three critical sync routes**
I need to implement the broker resolution endpoint (POST /api/v1/broker/resolve) and both sync routes (GET /sync/{resource}/changes and POST /sync/{resource}/ops). These form the communication backbone - the broker helps regions find each other, the GET route lets them discover what's changed, and the POST route applies those changes. I'll tackle them in that order since the broker is what kicks off the whole flow.

**Build out the ChangeLogEntry and OutboxEntry models**
Before my routes can do anything useful, I need the data models that track what's changed and what needs to sync. The ChangeLogEntry captures the actual changes to domain entities, while OutboxEntry manages the reliable delivery pattern. I'm following Porto architecture here, so these go in the appropriate container with proper separation of concerns.

**Wire up the changelog scheduler**
Once I have the models and routes, I need to register the sync job in ConsoleKernel so it actually runs. This is what turns the whole system from manual API calls into an automated sync mechanism that keeps my regions consistent without me babysitting it.

## Housekeeping

**Tackle the failing PHP test**
I've got one test failing out of 2,839, which is a 96.1% pass rate. That's close enough to perfect that the single failure is probably something silly I can knock out quickly. I should identify what's broken and fix it before it gets buried under new work.

**Clean up SendAnomalyAlertJobTest.php PHPStan errors**
This file is my top PHPStan offender with 67 errors. Since I'm in a good flow today with fresh work, spending 30 minutes here would give me a nice break between route implementations and chip away at that 9,206-error mountain. Plus, test files should be cleaner - they're documentation as much as verification.

## Parked

Nothing's explicitly blocked right now, which is nice. I'm consciously setting aside the token expiry enforcement and the domain table migrations for now - those feel like they want the routes and models solidified first. The migration especially needs me to understand the data flow before I start adding columns to production tables.