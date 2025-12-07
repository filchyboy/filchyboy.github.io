---
layout: post
title: "Daily Plan - 2025-12-07"
date: 2025-12-07
---

# Daily Plan - Sunday, December 07, 2025

## Today's Theme

I need to close out the Jest testing work that's been hanging and then dive into the cross-regional sync routes. The broker and sync endpoints are the critical communication layer for the whole CRS feature, so getting those established will unlock a lot of downstream work.

## The Main Work

**Finish the Jest PR review and merge**  
I've got the debug-jest-tests work sitting in PR status. I need to do a final review, make sure everything looks clean, and get it merged. This has been blocking my ability to confidently say our frontend tests are in a good state, and I don't want it to linger into another week.

**Build out the broker route (POST /api/v1/broker/resolve)**  
This is the entry point for cross-regional conflict resolution. I'll need to set up the controller, wire up the routing in Porto style, and make sure it's structured to handle the conflict resolution payload. This is foundational - without this endpoint, the regions can't talk to each other about conflicts.

**Create the sync changes route (GET /sync/{resource}/changes)**  
Once the broker route is in, I'll tackle this one. This endpoint lets regions query what's changed since their last sync. I'm thinking about how to structure the resource parameter and what the response format should look like - probably need to lean on the ChangeLogEntry model concept even if I'm not building that model today.

**Implement the sync operations route (POST /sync/{resource}/ops)**  
This is the companion to the changes route - it's how regions push their operations to be applied elsewhere. These two routes together form the core sync mechanism, so getting both of them done today would put me in a really strong position for the rest of CRS implementation.

## Housekeeping

**Tackle some of those ESLint errors in index.ts**  
88 errors in one file is pretty brutal. I should spend 30-45 minutes cleaning up what I can - probably a lot of type issues or unused imports that accumulated. Even if I don't fix all 88, making a dent will help me feel better about the frontend codebase health.

**Review the test-refactor planning directory**  
It's sitting in "Needs Work Units" and references the Porto container boundaries. Since I'm doing Porto-compliant work today anyway with these routes, I should read through what's documented there and see if I can sketch out a few work units. Maybe I'll even identify something small I can knock out as part of my route work.

## Parked

There's a whole queue of CRS work waiting (token expiry, the model creation for OutboxEntry and ChangeLogEntry, the scheduler registration), but I'm deliberately focusing on the API surface today. Those models and jobs won't matter if the routes aren't there to expose the functionality. I'll get to them once I have these three routes working and tested.