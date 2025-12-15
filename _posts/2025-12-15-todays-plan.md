---
layout: post
title: "Daily Plan - 2025-12-15"
date: 2025-12-15
---

# Daily Plan - Monday, December 15, 2025

## Today's Theme
I need to push the DSR security feature across the finish line for Phase 7. I've got four actions in progress that are all interconnected, and I want to close them out as a cohesive unit today. If I can get those wrapped up and verify the acceptance criteria, I'll have a complete security workflow ready to test.

## The Main Work

**Finish the DSR submission workflow**
I've got three actions partially built—`SubmitDSRRequestAction`, `SendVerificationEmailAction`, and the `SubmitDSRRequest` form request. These need to work together seamlessly, so I'll finish implementing them in sequence and make sure the validation flows correctly from the form request through to the actions. This is the core user-facing workflow for data subject requests, so getting it right matters.

**Complete the performance baseline tests**
I started these to make sure the DSR system can handle reasonable load without degrading. I need to finish writing the test scenarios and establish what "good" looks like for response times. This will give me a reference point if performance issues crop up later.

**Verify Phase 7 acceptance criteria**
Once the actions and tests are done, I'll methodically go through the Phase 7 acceptance criteria document and check off each requirement. I want to make sure nothing's been overlooked before I consider this phase complete. Better to catch gaps now than during integration.

**Guard the build health dashboard behind a feature flag**
This is from a different feature set, but it's straightforward and important. The unified build health dashboard shouldn't be visible to everyone yet—I need to add the feature flag guard so I can control rollout. This should be a quick win that makes the system more resilient.

## Housekeeping

**Tackle some of the FluentCrmAdapter PHPStan errors**
FluentCrmAdapter.php is sitting at the top of the PHPStan offenders list with 37 errors. I don't need to fix all of them today, but I should knock out at least a handful while I'm in the codebase. Even fixing 5-10 would make a dent and improve type safety in a critical integration point.

**Review the test-refactor planning directory**
This directory has research done and references ADR-0001 about container boundaries. I should read through what's there and see if I can draft an implementation plan. My test structure needs work, and having a clear plan will make it easier to chip away at this over time.

## Parked

Nothing's technically blocked right now, which is good. I'm deliberately setting aside the accessibility report for location views and the Groundhogg idempotency work—both are priority 1, but they require fresh mental space that I don't have today while I'm finishing DSR security. The configuration opportunities work (helpers, policy, seeder) is also going to wait until I've closed out this phase completely.