---
layout: post
title: "Daily Plan - 2026-03-25"
date: 2026-03-25
---

## Today's Theme

I'm staring at a mountain of untracked commits (490 across infrastructure, config, and other work) that tells the real story of where my attention has been. The test-remediation-harness has strong momentum with 23 commits this week, but I haven't touched it in 4 days and need to get back in there. I'm also noticing the production-readiness work got my attention just yesterday, which suggests my brain is shifting toward deployment concerns.

## The Main Work

**Reconcile the test remediation ledger baseline** - This has been nagging at me since the TestCase rebase broke the baseline tracking. I hate when my tools give me garbage data, and right now I can't trust what the harness is telling me about test failures. The 83% pass rate is already painful enough without wondering if the remediation queue is showing me real problems or phantom issues.

**Draft implementation plan for sanctum-security** - I keep seeing security gaps that make me nervous, and with all the production readiness work I touched yesterday, I'm in the right headspace for this. Better to plan the security work properly than hack something together when I'm under pressure later.

**Add MAX_PER_PAGE constants to ApiController** - Someone could theoretically request a million records through our pagination endpoints right now, which is the kind of oversight that would ruin my day if it happened in production. The risk-to-effort ratio here is compelling.

**Execute the remediation sweep through the failing test queue** - Assuming I get the baseline reconciled, I want to actually run this thing and see what breaks. I built this harness to automate test fixes, and I'm curious whether it'll actually work or if I've been building an elaborate procrastination tool.

## Housekeeping

**Run `make lint-fix` to clear those 2 auto-fixable ESLint warnings** - One command, immediate improvement in the noise level.

**Regenerate the route health report** - It's 60 days stale, and if I'm thinking about production readiness, I should probably know which routes are actually working.

**Hash out the stableHash utility function design** - The widget cache optimization has been sitting there, and cache invalidation bugs are the worst kind of debugging hell. Getting the hash function right from the start saves future pain.

## Parked

The thin vertical slice work (TV277, TV278) can wait until I'm back in feature development mode. Right now my brain wants to solve infrastructure problems, and fighting against that instinct usually leads to half-finished work across too many domains.

I'm also ignoring that massive markdownlint debt (11,482 issues) today - documentation quality matters, but not more than having reliable tests and secure APIs.

<!-- SCORE: 3.4 -->