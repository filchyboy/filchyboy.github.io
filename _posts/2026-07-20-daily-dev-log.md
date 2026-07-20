---
layout: post
title: "Daily Dev Log - 2026-07-20"
date: 2026-07-20
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-07-20T14:24:22.983173+00:00 -->

## Today's Plan

Monday. A lot landed yesterday — the federated knowledge architecture Phase 0 artifacts, the subtenant acquisition marketplace remediation, and a stack of feature sets that are now archived as complete. The board is substantially cleaner this morning, which means I can be deliberate about what I pick up next.

### Main Focus

**Continue the PHPStan remediation, starting with `phpstan-custom-guardrail-findings`.** I worked this yesterday and have been heads-down on it all week. The plan is at 3/16 units complete with 11 in progress, and the level-9 error count is sitting at 79. The guardrail findings are still the right entry point — not because they're the most numerous, but because they're violations of contracts I wrote explicitly. If I move into the type-shape wave while those are active, any repair I make in Ship or Compliance has compound attribution problems. Did I fix the type mismatch, or did I just remove the signal that exposed it? That's a debugging hole I'd rather not climb out of. After the guardrail surface is clean, `phpstan-type-shape-ship-compliance` is the natural next step — Ship and Compliance first, in line with how I've been ordering the wave all week.

**Open the `consent-authority-provider-integration-follow-on` work with `capi-s1-state-purpose-enums` and `capi-s1-permission-registry`.** This plan is one day old with 0 of 73 implementation units complete, and I touched it yesterday. The planning decisions are resolved — the design is settled around the governed authority lifecycle, API only, with the first delivery boundary explicitly scoped. Starting with `capi-s1-state-purpose-enums` and `capi-s1-permission-registry` is the right sequence because the enum definitions and the three registered permissions are what everything else in the lifecycle slice composes against. The lifecycle event schema (`capi-s1-lifecycle-event-schema`) can't be written cleanly without knowing the state and purpose vocabulary. This is also the place where I'll see whether the prior canonical tracer work from PR #4752 actually resolves the boundary questions the 17 deferred rows were pointing at — I expect most of them to be cleaner now, but I'm not certain until I'm in the code.

**Settle `capi-s1-authority-schema` and `capi-s1-authority-policy`.** These are the structural and enforcement pieces that follow naturally from the enums and permissions. The append-only event schema and the tenant-bound policy belong together in a single session because the schema migration has to exist before the policy can reference it for enforcement. If I do the schema without the policy in the same pass, I'll have a half-configured lifecycle that passes unit tests but doesn't actually enforce anything against real tenant boundaries. The risk of leaving that open is that something else lands against develop in the meantime that assumes the enforcement is live.

### Secondary Work

**Run `make sync-routes` to refresh the route health report.** The current snapshot is 23 days old — the report shows 3,447 routes with a failing status, but after the volume of work that's landed since then (role-assignment-audit, policy-center, ecommerce-source-onboarding, and more), that number is almost certainly stale in both directions. I won't know what's actually failing until I regenerate it.

### Maintenance

**Refresh the TODO inventory.** The last snapshot is 35 days old. Given the scale of refactoring that's happened in that window — the imperative-to-declarative sweep, the scoped tenant execution adoption, the tracker hygiene pass — the current count of 0 tracked items is not credible. Running the todo-cleanup script will either confirm it's genuinely clear or surface items that got introduced during those refactor waves.

**Draft the implementation plan for `capi-s1-revoke-command` and `capi-s1-proposal-command`.** These are the two command implementations in the consent authority follow-on that close the first delivery boundary. The planning pipeline shows 73 units in the feature set and the design decisions are resolved, so sketching the command boundary artifacts now — before I'm mid-way through the schema and policy work — means the command implementation session won't start with a blank page. The proposal command is the one I'm less certain about at the execution level: evidence-pinned commands have some ambiguity around how pinning is verified at the boundary versus at persistence time, and I want that decision written down before I'm writing tests against it.

**Check PHPStan error attribution after `phpstan-custom-guardrail-findings` clears.** Once the guardrail surface is clean, the reported 79 errors will redistribute across the remaining categories. Before I move into the type-shape wave in earnest, I want to verify the attribution is what I expect — that the guardrail clearance actually reduced the count rather than revealing errors that were previously obscured. This is a five-minute verification step that's caught attribution surprises before.

**Scan for Markdownlint issues in any planning files touched today.** The consent-authority plan docs and any PHPStan remediation planning artifacts I modify today are already open — checking those for Markdownlint cleanliness while they're in front of me is less effort than a separate pass later.

### Parked

The `react-doctor-100-followup-sprint-v2` work — clearing the 321 remaining State & Effects warnings — is parked today. It's not blocked, but it's the only item in that feature set and it's a context switch away from both the PHPStan remediation and the consent-authority lifecycle work I'm prioritizing. The two active threads have clear sequencing constraints between their own units; adding a third domain right now means none of them get the consecutive attention they need.

The `deepsec-run14-external-evidence-follow-up` plan and `dsr-fulfillment-browser-proof` are both in the pipeline and unblocked, but they've been at 0 units complete for a while without me creating a specific blocker — they're just genuinely lower leverage than what's on the board today. I'll revisit when the consent-authority first delivery boundary is further along.

<!-- plan-unit-ids: capi-s1-permission-registry,phpstan-report-visibility-ratchet,phpstan-type-shape-mcp-etl,phpstan-type-shape-userworkflow-logging -->
<!-- SECTION: DAILY-PLAN END -->

<!-- Generated by dev-tracker build_today_plan.py -->
