---
layout: post
title: "Daily Plan - 2026-03-25"
date: 2026-03-25
---

# Daily Plan - Wednesday, March 25, 2026

## Today's Theme
I'm staring at a massive test failure rate (31% passing) and realizing I can't keep building features on top of a crumbling foundation. The test remediation harness has been my biggest investment this week with 36 commits, but I haven't touched it in 4 days. Time to get back in there and actually drive it through the failing tests. Plus, I'm curious about those production readiness tasks I touched yesterday - might be time to tackle the boring-but-critical infrastructure work.

## The Main Work

**Reconcile the remediation ledger baseline and execute the sweep** - This test situation is genuinely frustrating me. I built this whole harness to systematically fix failing tests, then walked away from it. The ledger got stale after the TestCase rebase, and now I have 2,537 failed tests mocking me every time I run the suite. Time to stop procrastinating and actually use the tool I built.

**Configure TRUSTED_PROXIES for production** - I was poking at the production-readiness work yesterday, and this one's been nagging at me. If I deploy with the wrong proxy configuration, requests are going to have completely wrong IP addresses and security checks will fail in weird ways. Better to get this boring config work done now than debug it at 2 AM when something breaks.

**Add the pagination constants to ApiController** - I keep seeing pagination implemented inconsistently across controllers, and it's the kind of technical debt that compounds. MAX_PER_PAGE and DEFAULT_PER_PAGE constants will force some consistency. This needs focused attention to get the boundaries right - too low and the API feels sluggish, too high and we risk performance issues.

**Create the stableHash utility function** - The widget cache keys have been a mess, and I've been putting off this refactor for too long. Cache invalidation is already hard enough without unpredictable key generation making it worse. This utility should be straightforward to implement, but getting the hashing algorithm right matters for cache hit rates.

## Housekeeping

**Run `make lint-fix` to clear those 2 auto-fixable warnings** - Might as well clean up the noise while I'm thinking about code quality.

**Refresh the route health report** - It's 60 days stale, which is embarrassing. A quick `make route-health-check` will give me current data on what endpoints are actually working.

**Draft an implementation plan for the sanctum-security work** - Since I'm already thinking about production security with the proxy config, I should map out the token authentication hardening while the security mindset is active.

**Update the TODO inventory** - 62 days old is pretty bad. The `todo-cleanup` script will show me what technical debt I've been ignoring.

## Parked

The thin vertical slice work is tempting since I have contract scope baselines ready to go, but I'm not going to start new feature development when my test suite is this broken. The eager loading N+1 fix can wait too - performance optimizations don't matter if the code doesn't work reliably first.

I'm also deliberately avoiding the compliance audit work even though it showed up recently. That's going to require deep focus and probably uncover a bunch of gnarly edge cases. Not the right headspace for that today.

