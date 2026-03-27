---
layout: post
title: "Daily Plan - 2026-03-27"
date: 2026-03-27
---

## Today's Theme

I've got two momentum builders converging today - the production readiness work I touched yesterday (fresh security configuration thinking) and the PHPStan remediation that's been sitting there taunting me. With 1796 failing tests staring at me, I want to see if this remediation harness actually works or if I built an elaborate system to disappoint myself.

## The Main Work

**Execute that remediation sweep I've been avoiding** - I touched the test harness yesterday and honestly, I'm tired of having this infrastructure sitting there unused. The failing-file queue is loaded and ready. Time to see if my harness design actually works or if I need to go back to the drawing board. I'm genuinely curious what patterns will emerge.

**Lock down TRUSTED_PROXIES for production** - Security configuration is one of those things that makes me paranoid in the best way. I was thinking about this yesterday, so all the proxy patterns are bouncing around in my head. Getting this wrong in production means debugging at 3 AM when everything breaks spectacularly.

**Finish the migration schema squash** - This is foundational cleanup that I keep putting off. Database migrations are like technical debt - ignore them long enough and they become a crisis. I need this baseline clean before the production deployment, and it's been nagging at me for days.

**Start TV277 contract scope baseline** - I haven't touched this thin slice in 5 days, which means the context is completely cold. But getting the contract boundaries locked down early prevents the scope creep that always kills these projects. Better to define what I'm building now than argue about it later.

## Housekeeping

**Regenerate that ancient route health report** - 62 days stale is embarrassing. One `make route-health-check` command will tell me what's actually broken versus what's just old data. I'm curious if those 1691 routes are really failing or if it's just stale noise.

**Run the TODO cleanup script** - 64 days without refreshing the TODO inventory is terrible project hygiene. The `todo-cleanup` script should surface what's actually relevant versus what's just archaeological artifacts.

**Draft sanctum security implementation plan** - Since I'm already thinking about security with the trusted proxies work, this flows naturally. Having the research done means I can turn it into concrete work units.

## Parked

The eager loading N+1 fixes can wait - I need to see some wins on the production readiness front before I dive into performance optimization. Also not touching the API pagination guardrails until I have a clearer picture of what the actual usage patterns look like.

## Open Questions

Will the remediation harness actually find actionable issues, or did I build an elaborate way to generate more noise? And why do I have zero files tracked in my codebase metrics - that seems like a measurement problem worth investigating.

