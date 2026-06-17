---
layout: post
title: "Daily Dev Log - 2026-06-17"
date: 2026-06-17
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-06-17T15:06:05.604136+00:00 -->

## Today's Plan

Yesterday went somewhere completely different from what I'd mapped out — the org learning lifecycle turned into a full vertical slice, from DTOs and enums through query tasks, classifiers, aggregation services, and the API endpoint, all the way to the frontend dashboard component. That's done and merged. Today I'm returning to the contracts and boundary work that's been queued.

### Main Focus

**Draft `mgp-boundary-adr` for Model Governance Plane** — The restructuring from earlier this week — splitting ownership across `Core/ModelGovernance`, `Core/ModelRegistry`, and `Agent/AgentRuntime` — needs to be captured as an architectural decision before implementation begins. That split is the kind of thing that's obvious right after you make it and murky three months later when someone asks why registration lives in AgentRuntime and admission lives in ModelGovernance. The ADR is the unblocking first step for all 34 tracker items in this plan. The design is settled; this is about recording it.

**Begin the content provenance contract sequence, starting with `cpdcp-module-interface-contract`** — The planning pipeline lists this as the next ready unit, and it's the right entry point: the module interface contract defines how external callers interact with the CPDCP boundary, which determines the surface area that the authorship classification contract, the regulatory authority contract, and the publication preflight contract all have to conform to. Starting with authorship classification instead risks writing a contract that doesn't fit the module interface once that interface is defined. The 54-unit plan is at 0% and has been ready since June 14 — the sequencing here actually matters, and I want to get it right.

**Complete the three in-progress PHPStan baseline remediation items** — `phpstan-baseline-freeze-2026-06-14`, `phpstan-archive-superseded-remediation-maps`, and `phpstan-promote-harness-reference` are all actively in progress. The freeze is the linchpin: without a frozen baseline snapshot from June 14, I can't run meaningful diffs as I work through the 7,093 errors in the current report. The archive and harness reference promotion are smaller but they clear the Phase 1 board entirely, which means Phase 2 type-shape repairs can start without unresolved Phase 1 state cluttering the tracking.

**Draft `cpdcp-authorship-classification-contract`** — Once the module interface contract establishes the CPDCP boundary shape, the authorship classification contract defines the core taxonomy. This is where the vocabulary gets set: what constitutes AI-generated content, human-authored content, hybrid content, and how those categories get represented in the type system. Everything downstream — regulatory authority rules, publication preflight decisions, enums — references these definitions. Getting the classification contract drafted while the module interface is fresh in my head is more efficient than returning to it cold.

### Secondary Work

**Start `cpdcp-regulatory-authority-contract`** — If the authorship classification contract lands cleanly, the regulatory authority contract is the logical next step in the same sequence. It defines which rule authorities have standing to make publication decisions for each authorship classification. The dependency chain here is explicit: authority contracts need the classification vocabulary to reference.

### Maintenance

**Run `todoremed-p0-replace-template-boilerplate`** — The todo-remediation planning directory has template boilerplate still in place and 0 tracked items done. This is a short task that cleans up the planning directory structure and is worth doing before the todo-remediation work gains momentum. It's been sitting with no activity.

**Check the 50 PHP test failures for environment failures** — The test suite is at 0% pass rate across 50 tests, which is almost certainly not 50 real regressions — that pattern usually means a bootstrap or environment issue is cascading. Worth running the suite locally and seeing how many failures share a common root before treating them as individual bugs. If it's environmental, one fix clears the board; if it's real regressions, I need to know that before I keep adding implementation.

**Markdownlint pass on content provenance planning files** — I'll be editing the CPDCP planning directory today. The markdownlint report shows 175 issues across 11 files, and there's a good chance some are in planning files I'll already have open. A targeted pass on the files I touch costs almost nothing and keeps the issue count from growing.

**Draft implementation plan for `erx-bundle-execution-contract`** — The evaluation registry expansion roadmap has 13 tracked units and is aligned with the governance work I've been on this week. The next unit, `erx-bundle-execution-contract`, is a contract definition — the same kind of work I'm doing today in content provenance and model governance. Planning it now while I'm thinking through contract structure means I'm not starting from zero when I get there.

### Parked

**`react-doctor-100-followup-sprint-v2`** and **`frontend-loc-remediation-followup`** — both are queued and neither is blocked, but the day is already structured around contract definition and PHPStan remediation. Frontend remediation work requires a different kind of attention and I don't want to split that across two different domains in one day. These are concrete candidates for tomorrow if the contract sequence goes well today.

**`todo-remediation` main body** — beyond the boilerplate cleanup, the 68-unit todo remediation plan needs a proper planning pass before I start working through it. The boilerplate task today is a precondition; the actual remediation work comes after.

<!-- plan-unit-ids: cpdcp-module-interface-contract,erx-agenteval-consumption,erx-bundle-execution-contract,erx-tsra-drift-contract,mgp-boundary-adr,phpstan-baseline-freeze-2026-06-14,rd100v2-regression-and-ruleset-diff,todoremed-p0-replace-template-boilerplate -->
<!-- SECTION: DAILY-PLAN END -->

<!-- Generated by dev-tracker build_today_plan.py -->
