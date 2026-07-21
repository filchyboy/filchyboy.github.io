---
layout: post
title: "Daily Dev Log - 2026-07-21"
date: 2026-07-21
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-07-21T13:14:39.428499+00:00 -->

## Today's Plan

Tuesday. Yesterday's work went everywhere — consent authority lifecycle, vertical proof slices, DSR fulfillment, checkout payment flows, procedural brandmark research, and a dozen other threads. The PHPStan remediation and the imperative-to-declarative refactor plan are both technically unfinished but both got real attention. Today I want to close at least one of them out, or at least get past the first meaningful gate.

### Main Focus

**Execute `idr-00-baseline-characterization` and then `idr-01-browser-privacy-disposition-rules`.** The imperative-to-declarative refactor plan is one day old, 0/13 tasks complete, and I worked on it yesterday. The baseline characterization is the literal first gate — it captures current behavior for all ten refactor candidates, which is what makes the subsequent refactors safe to execute without guessing about regressions. I can't write a meaningful test assertion for `idr-01` without knowing what the browser privacy admission code actually produces today. The refactor target there is converting the conditional-chain in the privacy disposition logic into an ordered set of rule descriptors, and the decision about where to capture that baseline (integration test boundary vs. unit characterization test) is genuinely open. My instinct is the integration boundary, because the browser privacy code touches the `BrowserPrivacyDispositionRules` evaluator and the admission pipeline — a unit test could pass while the pipeline composition breaks. That instinct needs to survive contact with the actual code.

**Move through `phpstan-custom-guardrail-findings` and into `phpstan-type-shape-ship-compliance`.** PHPStan is at 122 errors at level 9 and this has been the dominant thread all week. The custom guardrail findings have to clear before the type-shape wave is interpretable — violations of my own project-specific contracts compound with type-shape errors in ways that make attribution genuinely ambiguous. If I patch a type mismatch in a Ship container while a guardrail violation in the same file is producing a phantom error, I can't tell which change produced which delta in the report. The guardrail surface is the precondition, not just the preference. After that clears, `phpstan-type-shape-ship-compliance` is the ordered next step based on the wave sequencing I've been maintaining.

**Work through `doc-audit-2026-07-21-dha-023-planning-links` and `doc-audit-2026-07-21-dha-024-code-references`.** The documentation audit batch started today, 0/10 units complete, with `DHA-023` as the explicitly ordered first item. `DHA-023` retargets architecture work links that currently point at planning files rather than completed-plan evidence — this matters because those links are cited in docs that I may be touching during the refactor and remediation work today. A broken reference in documentation that's actively being read is a different category of problem than a stale link in an archived doc. `DHA-024` normalizes Laravel code-reference links and has a logical dependency on `DHA-023` in the Phase 1 sequencing. These two are bounded enough that they shouldn't derail the main focus.

**Start `tv555-contract-scope-baseline` for the workspace approval inbox live loop.** This was the first unit completed yesterday — the journey contract is frozen — which means the remaining seven units in that feature set are unblocked and waiting. The contract baseline being done changes the nature of the next steps; they're now execution against a known surface rather than discovery work. This is the right time to look at what `tv555` needs next and whether any of the backend or API units can move today.

### Secondary Work

**Run the `idr-11-focused-quality-gates` pass on any files touched during the declarative refactor work.** This is explicitly a post-refactor step in the plan and is worth running before the day's work is committed — catching quality regressions at the file level rather than letting them accumulate into the PHPStan baseline.

**Scan the `rd100v2-state-effects-warnings-wave` item** in the react-doctor sprint. There are 321 State & Effects warnings sitting outside the Phase 1 hotspots and this feature set has had no recent activity. I'm not committing to it today, but understanding what the warning distribution looks like in those files would tell me whether this is a mass-mechanical fix or a set of architectural decisions. That distinction matters for sequencing it against the ESLint fixable-warning count (5,535 fixable warnings currently flagged).

### Maintenance

**Refresh the route health report.** The last snapshot is 24 days old. `make sync-routes` is a single command and the report feeds into the quality picture I'm working against. 3,447 routes with an unknown current-state failure profile is a gap worth closing, especially with the workspace approval inbox work active.

**Refresh the TODO inventory.** 35 days since the last run. This one I'm less certain about — the last run found 0 tracked items, which either means the codebase genuinely has no TODO debt or the tool's scope excludes patterns I'm using. Running it now at least gives me a current baseline.

**Draft the implementation plan for `dtpr-run-contract`** — the dev-tracker publication run is 4 units unstarted and the next item is the run contract definition. This is aligned with the build-in-public work that's been a background thread all week, and the planning artifact is the gate that makes the rest of the publication run executable.

**Check markdownlint issues in any documentation files touched during `DHA-023` and `DHA-024`.** The documentation audit work will produce file changes in the docs hierarchy. Running markdownlint scoped to those files before committing avoids accumulating lint debt in the exact files I just fixed.

### Parked

The `react-doctor-100-followup-sprint-v2` main wave (`rd100v2-state-effects-warnings-wave`, 321 warnings) is not a priority today because I haven't characterized whether those warnings are mechanical or structural. Attacking 321 warnings without that distinction produces changes I can't evaluate. It's parked until I have a clearer read on the distribution.

The `deepsec-run14-external-evidence-follow-up` plan (`run14-external-evidence-source-reconciliation` as the next unit) has been waiting for a session I haven't given it yet. The 122 PHPStan errors and the declarative refactor work are higher leverage today, and the deepsec work has no external deadline surfaced. It'll come back up when the PHPStan surface is cleaner.

<!-- plan-unit-ids: doc-audit-2026-07-21-dha-033-freshness-signal,phpstan-report-visibility-ratchet,phpstan-type-shape-mcp-etl,phpstan-type-shape-ship-compliance -->
<!-- SECTION: DAILY-PLAN END -->

<!-- Generated by dev-tracker build_today_plan.py -->
