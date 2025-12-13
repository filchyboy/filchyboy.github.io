---
layout: post
title: "Daily Plan - 2025-12-13"
date: 2025-12-13
---

# Daily Plan - Saturday, December 13, 2025

## Today's Theme
I'm wrapping up the DSR security work that's been in flight and pushing to get Phase 7 completely done. I've got four tasks already in progress, and I want to close them out properly rather than letting them linger into next week. It's Saturday, so I'm treating this as a focus day without interruptions.

## The Main Work

**Finish the three DSR actions I've started**
I've got SubmitDSRRequestAction, SendVerificationEmailAction, and the SubmitDSRRequest form request all partially built. These are interconnected pieces, so finishing them together makes more sense than context-switching. The form request validates incoming DSR submissions, the submit action orchestrates the workflow, and the email action handles verification tokens. I need to wire them up properly and make sure they follow Porto's Action/Task separation correctly.

**Complete the performance baseline tests**
I started these but need to finish establishing solid baselines for the DSR submission flow. This is important because I want to catch any performance regressions early, especially around email sending and database writes. I'll set up tests that measure response times and query counts so I have objective data to work with.

**Verify Phase 7 acceptance criteria**
Once the actions and tests are done, I need to methodically go through the acceptance criteria checklist for Phase 7. I've been heads-down implementing, but I need to step back and make sure I actually completed what I set out to do. This includes checking security boundaries, error handling, and integration points.

**Generate accessibility report for location views**
This is a priority 1 task that's been waiting, and it's only an effort-1, so I should be able to knock it out. The location views are user-facing and the overall accessibility score is sitting at 30%, which is terrible. Running this report will give me concrete violations to address and help me understand where the biggest gaps are in that specific area.

## Housekeeping

**Address some PHPStan errors in SendAnomalyAlertJobTest.php**
This file has 67 errors and it's at the top of the offenders list. Since I'm already in testing mode with the performance tests, it makes sense to spend some time here cleaning up type issues. I don't need to fix all 67, but I can probably knock out the low-hanging ones while my head is in test-land.

**Review the test-refactor planning directory**
This needs an implementation plan, and it's directly relevant to the testing work I'm doing today. ADR-0001 requires container-scoped `Tests/` directories, and I should understand what that migration looks like before I write too many more tests in the old structure. I'll read through the research and maybe draft some notes about the implementation approach.

## Parked

Nothing is technically blocked right now, but I'm deliberately not touching the configuration-opportunities work (the helper methods, RBAC policy, seeder extension). Those are all effort-3 tasks and I want to finish the DSR phase cleanly before opening up a new can of worms. The session security and COPPA migrations can wait until I've cleared my in-progress queue.