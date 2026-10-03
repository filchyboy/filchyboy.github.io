---
layout: post
title: "Week 40 Retrospective"
date: 2026-10-03
categories: [weekly, retrospective]
tags: [build-in-public, weekly-digest]
---

## The Big Picture

Week 40 was a sprawl week — high throughput, low plan adherence, and a breadth of surface area touched that reflects a platform being pulled toward readiness across many axes simultaneously. The two planned anchors, security review remediation and agent auth audit remediation, did get done, but they were outnumbered by the unplanned work that accumulated around them.

## What Happened

The week opened with the security review remediation flush. Eighty-three items across a single active day is the kind of throughput that happens when you've been carrying a backlog of known issues and finally dedicate a session to clearing it. The agent auth audit remediation ran parallel across five days — slower, more deliberate, which reflects the nature of that work: auth surfaces require verification at each step rather than bulk closure. Both of these were planned, and both delivered.

What wasn't planned was the volume of everything else. Privacy ran across five days and produced 43 completions. Decisions, billing, scenarios, and MCP each ran for most of the week, collectively accounting for well over a hundred items. The existing-feature-completion batch on October 1st — 41 items in a single day — reads like a deliberate sweep of known gaps rather than discovery work. The codebase maturity pilots also moved: billing read consoles, booking query pilot, checkout confirmation, tenant booking list, and billing account identity all saw completion batches. That's a meaningful structural investment — those maturity passes are how the codebase earns the right to be extended rather than constantly apologized for.

Wednesday the 29th was the outlier, 87 completions against the week's average of 147. It's the day the plan called for admission inventory allocation and synthetic scenario work — neither of which moved. That's not a productivity dip so much as a day where what was planned and what was executable were misaligned. The plan had scheduled work that wasn't ready, so other things filled the space.

The accessibility baseline work is worth addressing directly. Two feature sets — accessibility-baseline-01-reported and accessibility-baseline-02-recovered-stories — had 39 items progress without a single completion. That pattern means stories were recovered, staged, or categorized but not resolved. Combined with the thin vertical slices across CDP contact profiles, billing report generation, budget threshold editing, and agent registry configuration, there's a picture of a week where the platform's feature surface was being audited and rationalized as much as it was being built. That's appropriate at this stage, but it does mean a portion of the week's energy went into work that won't show up as shipped until a future week.

## Axes Covered

Security and auth hardening anchored the planned work, with the CSP remediation for admin shell (`unsafe-eval` retirement via flag and then direct fix) representing the kind of cleanup that has to happen before any future operator relies on these policies. Privacy and compliance moved steadily across the week. MCP was active all six days, which reflects ongoing investment in the agent layer's protocol surface. The codebase maturity pilots touched booking query, billing consoles, checkout confirmation, and admin page shell, each following the same pattern: a concentrated burst over one or two days. Browser experience closeout and surface ownership baseline remediation both closed in a single day, suggesting they were well-bounded cleanup tasks. Billing, scenarios, and decisions ran the full week without completing everything, which is consistent with these being active development axes rather than maintenance sweeps. Intelligence and CDP had quieter contributions — present but not dominant. The thin vertical slices for agent tracing, regulatory rule lookup, Slack channel health, and contact field history all produced completions, which means the agent intelligence surface continues to accumulate breadth even when no single slice is the week's focus.

## Under the Radar

Three hundred ninety-one commits didn't map to any tracked feature set, and that's not a tracking failure to apologize for — it's the nature of a platform being built and maintained at the same time. The token system work (`PrimitiveSpacingTokens` half-step keying, nested `tokens.json` group unwrapping, the pre-commit exclusion for token sources) represents design system stabilization that rarely gets a dedicated tracker but compounds in value every time a new UI surface is built. The CSP fix for `unsafe-eval` in the admin shell appeared in both the tracked and untracked commit logs, which suggests it crossed boundaries as the remediation progressed from flag-controlled rollback to permanent retirement. Dependency bumps for CodeQL and both the npm and composer groups are maintenance I'd rather have automated and invisible, and they largely are, but they're still real work. The `APP_URL` domain registration on deploy and the tenant requirement enforcement on registration are the kinds of behavioral changes that only matter once the platform is running with real tenants, but getting them right now means they won't be discovered as gaps later.

## Looking Ahead

The three planned feature sets that saw zero progress all week — admission inventory allocation, events scheduling shared contracts, and external event graph consumption — have now appeared in plans across multiple days without movement. At some point that's a signal worth taking seriously: either these are blocked by something upstream that needs to be named explicitly, or they're lower priority than the plan has been treating them. I'd rather resolve that question before they accumulate another week of zero progress.

The accessibility baseline work that's sitting in progress rather than complete will need a dedicated push. Thirty-nine items progressed without resolution means there's a queue of known issues waiting for remediation work that hasn't been scheduled. The codebase maturity series still has the admin page shell pilot partially in progress and the capability review at zero — those are worth sequencing deliberately rather than letting them drift into the catch-all of a busy week.
