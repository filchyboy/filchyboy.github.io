---
layout: post
title: "Daily Dev Log - 2026-11-28"
date: 2026-11-28
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->

## Today's plan
*Recovery draft prepared this morning.*

The free appointment journey is still the shortest path to proving the first wedge end to end. Today’s priority is to get the staging fixtures admitted: two unrelated accounts, the people and calendars needed to exercise both, and a clear plan for cleanup. Once those are in place, we can test whether a customer can book and whether each business sees only its own records. The broader migration rehearsal is separate and shouldn’t hold up this proof. (`asie-staging-admission-and-fixture`, `asie-two-account-isolation`)

Paid appointments have moved from deciding how to price an offering to proving that a business owner can publish one through the normal setup flow. I’ll focus on the remaining publishing UI and the test that follows it: a business owner can publish at the intended price, a retry doesn’t create a second version, and a stale price is rejected without leaving a partial offering. That’s the next milestone, not a claim that payment or refunds are ready. (`agc-02-publication-ui`, `agc-02-publication-proof`)

The prospect work can move in parallel. I’ll pin down who should try the workflow, what decision they make today, and what would count as a successful appointment for them. That gives the staging test a business outcome to prove without asking a prospect to try an unverified workflow. (`appointment-qualified-prospect-proof-01`, `appointment-qualified-prospect-proof-02`)

<!-- SECTION: DAILY-PLAN END -->
