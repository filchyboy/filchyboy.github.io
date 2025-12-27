---
layout: post
title: "Daily Plan - 2025-12-27"
date: 2025-12-27
---

# Daily Plan - Saturday, December 27, 2025

## Today's Theme

I'm at an interesting crossroads today. The mcp-toon-integration work has been my main focus this week (56 commits!), but I touched the updated-comms-hub-work yesterday and have fresh context there. I'm going to split my day between wrapping up that last MCP scope violation test and then diving into the CDP adoption work for the comms hub. The CDP adoption tasks are all sitting at a score of 22.0 with maximum recency and momentum boosts - that's the system telling me I've got hot context and should capitalize on it.

## The Main Work

**Finish the MCP scope violation test** - This is the last item in the mcp-toon-integration feature set, and I've poured 56 commits into this work over the past week. My head is completely in the MCP security model right now, and leaving this test incomplete would mean losing all that context over the weekend. I need to create `MCPToonScopeViolationTest.php` and verify that the scope enforcement actually works as designed. Once this is done, the entire MCP integration can move toward completion.

**Create the marketing_audience_contacts pivot table** - I touched the updated-comms-hub-work today, which means the CDP adoption strategy is loaded in my brain right now. This pivot table is the foundation for migrating the Audience model away from the old contact structure to the new CDP\Contact model. The recency score of +5.0 is telling me to strike while the iron is hot - I have fresh context on both the old and new contact systems.

**Refactor the Audience model to use CDP\Contact** - This flows directly from creating the pivot table, and it's one of eight related tasks all scored at 22.0. The momentum score of +3.0 reflects that I've been actively working in this area. The Audience model is central to how the marketing features work, so getting this migration right will make all the downstream refactoring (ContactList, CampaignSend, WorkflowEnrollment) much smoother.

**Refactor the ContactList model to use CDP\Contact** - Continuing the CDP adoption momentum. Once I've done Audience, ContactList is the logical next step since these two models work closely together. I want to keep the refactoring pattern consistent across all these models while the approach is fresh in my mind. Breaking this up across multiple days would just mean re-establishing context each time.

**Start refactoring CampaignSend model to use CDP\Contact** - If I get through the first three, I'll tackle this one. It's the same pattern but applied to campaign sending logic. I may not finish it today, but getting it started while I'm in the zone means I won't have to rebuild as much context later. The momentum here is real - all eight tasks in this feature set are showing maximum behavioral scores.

## Housekeeping

**Review the Jest test failures** - I've got 23 failing tests out of 4,156, which is a 97.8% pass rate, but those failures could be masking issues in the CDP refactoring I'm about to do. Before I start moving models around, I should at least look at what's failing and make sure it's not in the Email or Marketing containers.

**Check the accessibility violations** - With a 30% score and 51 violations, this is pretty rough. I won't fix them all today, but I should at least run the accessibility audit on the components I touch during the CDP refactoring. If I'm already in those files, might as well clean up any obvious issues while I'm there.

## Parked

The **mcp-toon-guard-update** work needs to stay parked until I finish the scope violation testing - I can't update the guard logic until I know the current implementation is properly tested. The **test-refactor** planning directory is calling out that I need container-scoped test directories per ADR-0001, but that's a bigger structural change that doesn't make sense to tackle in the middle of this CDP adoption push. I'm also deliberately setting aside the ESLint errors (279 errors!) - those index.ts and ColorTokensSection.tsx files are a mess, but diving into frontend linting today would derail my backend refactoring momentum entirely.