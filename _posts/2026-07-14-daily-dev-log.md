---
layout: post
title: "Daily Dev Log - 2026-07-14"
date: 2026-07-14
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-07-14T13:13:30.317033+00:00 -->

## Today's Plan

Tuesday. Yesterday covered an enormous amount of ground across jurisdiction attribution, DSR fulfillment, cache key migration, structured logging, and price-change trust context — all of it shipped and merged. Today the PHPStan remediation is the thing I actually touched in the last 24 hours, and the deepsec evidence follow-up has been waiting since last week with nothing blocking it.

### Main Focus

**Move through the PHPStan type-shape wave: `phpstan-type-shape-ship-compliance` then `phpstan-type-shape-mcp-etl`.** The plan is 3/16 units complete with 11 in progress, sitting at 395 errors at level 9. I've had heavy focus on this all week and worked it yesterday. The ordering discipline is the same constraint I've been respecting throughout: type-shape repairs before runtime-shape repairs, because correcting call sites against imprecise property declarations just shifts errors laterally rather than eliminating them. Ship and Compliance are the right domains to start with — a significant portion of yesterday's DSR fulfillment and lifecycle work touched those containers, which means the property shapes are most likely to have drifted from their declared types. I'd rather reconcile that now, before the runtime-shape wave runs against a stale declaration surface.

**Pick up `run14-external-evidence-source-reconciliation`, then chain through `run14-openai-key-rotation-evidence` and `run14-openai-auth-routing-export-audit`.** The deepsec Run14 evidence plan has been active since July 10th, 0/5 complete, with no blockers — I just haven't given it a dedicated session. The scope is narrow and explicitly bounded: external evidence only, no application remediation (that's already archived with commit `82f403a832`). The reconciliation task confirms evidence scope and owners, which is the prerequisite for recording the key rotation evidence and auditing the local `OPENAI_API_KEY` export routing. Doing the reconciliation first matters because I don't want to record evidence artifacts against an unverified scope boundary and then need to retract them during the closeout step. Three items in sequence, no ambiguity about what "done" looks like.

**Start the agent enforcement boundary inventory: `agent-enforcement-boundary-inventory`.** This plan has been active since July 10th, also 0/5 complete, and the inventory task is the explicit prerequisite for the interface decision that follows. I'm genuinely uncertain about where the TrustFabric coupling currently lives — whether it's concentrated in a specific enforcement surface or distributed across policy admission points — and the inventory is how I find out. That answer directly determines whether the interface decision (`agent-enforcement-interface-decision`) ends up as a clean boundary extraction or something messier. Starting the inventory without prejudging the outcome is the right posture.

**Run `phpstan-refresh-report-wave-2`.** This is already in "Ready to Start" and exists specifically to capture the PHPStan error count after the runtime-shape wave lands. Getting the report refresh queued after the type-shape work gives me a clean checkpoint before I move into the runtime-shape units (`phpstan-runtime-shape-compliance-mcp-etl`). The 395-error count in the current report is from the level-9 snapshot — I want to know what the number looks like after today's type-shape repairs, not carry a stale baseline into the next phase.

### Secondary Work

**Advance `run14-backup-iam-evidence` and `run14-external-evidence-closeout` if the earlier deepsec items clear.** The closeout depends on the other four evidence items being recorded, so this is sequentially appropriate — if the morning session gets through reconciliation, key rotation, and the export routing audit, the backup IAM evidence and closeout are the natural continuation rather than a context switch.

### Maintenance

**Refresh the PHP test report.** The test results are 29 days old and sitting at 0% pass rate (0/50). That number is almost certainly environment drift or a stale fixture, not 50 genuine regressions — but I can't know that without running `make test-fixed-batches-quick`. Given how much has shipped in the past month, I'd rather have a current snapshot.

**Refresh route health.** The route health report is 17 days old against a codebase with 3,447 routes. Yesterday's DSR fulfillment and lifecycle modules added new routes; `make sync-routes` gives me a current baseline before I start the next domain.

**Draft the implementation plan for `scoped-tenant-execution-adoption-remediation`.** The planning pipeline flagged this as aligned with active remediation work. It's currently in "needs research" state. Given that the PHPStan remediation has been my primary quality axis this week, drafting the plan artifact for scoped tenant execution adoption while that domain is loaded is more efficient than coming back to it cold next week.

**Refresh the TODO inventory.** It's 28 days stale. The todo-cleanup script is a single command and gives me a current view of what's accumulated during the horizontal slice and vertical slice work that's been landing all week.

### Parked

The React Doctor follow-up (`rd100v2-state-effects-warnings-wave`) is parked — 321 remaining State & Effects warnings need attention, but diving into ESLint remediation while the PHPStan wave is mid-execution creates dual-front noise I'd rather avoid. The PHPStan type-shape and runtime-shape phases have a clear ordering dependency; fragmenting attention across both static analysis systems at the same time means neither gets a complete pass today.

The `production-readiness-reconciliation` plan (33 units, 0 done) is visible but I'm not starting it today. It's a broad surface and I haven't loaded the scope yet — pulling it in alongside an active evidence closeout and a PHPStan wave would just mean none of the three get adequate depth.

<!-- plan-unit-ids: agent-enforcement-boundary-inventory,phpstan-report-visibility-ratchet,phpstan-type-shape-ship-compliance,phpstan-type-shape-userworkflow-logging -->
<!-- SECTION: DAILY-PLAN END -->


<!-- SECTION: ACCOMPLISHED START -->
<!-- accomplished-generated: 2026-07-15T14:06:03.434443+00:00 -->
<!-- accomplished-updated: 2026-07-15T14:06:03.434443+00:00 -->

## Today's Update

Today was a documentation infrastructure day — specifically, closing out a two-track audit that had been running in parallel: hierarchy audit remediation and hierarchy audit reliability. Both are now archived.

The remediation track was the more mechanical of the two. It had accumulated a backlog of broken nav targets, stale frontmatter commands, and placeholder guidance that was technically present but not useful. I worked through it systematically: built a missing-target ledger for MkDocs first, then used that ledger to drive the actual nav repairs rather than hunting blind. The design-system navigation retargeting came out of that ledger directly. The high-confidence link repairs went in as a batch — the distinction between "high-confidence" and everything else matters here, because the remaining broken-link triage required judgment calls that don't belong in an automated pass. Those got documented in a separate manual triage artifact rather than resolved with a guess. Directory index coverage also improved across the maintained sections, and the documentation hub README got a full refresh to reflect the current state rather than the aspirational state it had been describing.

The reliability track ran alongside remediation and was about making sure the audit process itself is trustworthy going forward. I documented how deterministic automation handles memory paths — the point being that the next time this audit runs, it shouldn't depend on anyone remembering the implicit rules from the previous run. The finding ledger got rebuilt from the current branch rather than carried forward from a stale baseline, which matters because a ledger built on stale evidence will pass checks that should fail. The enforced link validation behavior is now defined as a contract with an explicit threshold and ratchet — meaning the link error count can only go down from the baseline, never up. That's a one-way gate, and I think it's the right design for a docs system where link rot tends to accumulate gradually rather than arrive in a single bad commit. Whether the threshold is calibrated correctly is something I'll only know after the next few audit cycles, but having a threshold at all is better than the previous situation where "link validation passed" was essentially undefined.

Outside the documentation audit work, a handful of other things landed. The price approval API call was updated to include step order and role requirements — that's a data-shape change that makes the approval flow less ambiguous when multiple steps are involved. The CTA retry and envelope job type reconciliation closed a gap in how those two job concepts relate to each other, which had been loose enough to cause confusion during implementation. I also added an imperative/declarative refactor skill to the MCP skill registry, which is the kind of thing that sounds minor but has real downstream impact: the automation now has a documented pattern for when to use an imperative rewrite versus a declarative transformation, rather than treating those as equivalent. The `locateExistingRun` rename from `findConflictingRun` in the persist method refactor is worth noting specifically — the old name implied the run was always in conflict, which was wrong; it's only a conflict if certain conditions hold, and the rename makes the intent clear before any future caller interprets it incorrectly.

Composer and npm dependency groups both got bumped, and the two planning archives went in cleanly. The hierarchy audit work is formally closed. The next meaningful question is whether the enforced link validation threshold survives the first automated run against the current branch — that's the first real test of whether the reliability track actually holds under pressure.

---
<!-- Generated by dev-tracker publish_to_jekyll.py (AI mode) -->
<!-- accomplished-date: 2026-07-14 -->
<!-- unit-ids: dhar-frontmatter-workflow-command,dharl-memory-path-contract,dhar-link-validation-policy,dharl-current-state-reconciliation,dharl-enforced-link-mode-plan,dhar-mkdocs-nav-ledger,dhar-design-system-nav,dhar-doc-hub-refresh,dharl-finding-ledger-reset,dharl-quality-gates-closeout,dhar-link-autofix-batch,dhar-user-facing-placeholders,dharl-link-validation-baseline,dhar-mkdocs-nav-repair,dhar-directory-index-coverage,dhar-link-manual-triage,documentation-complete-hierarchy-audit-remediation,cta-reconcile-retry-envelope-job-type,health-keep-idle-workers-ready,price-approval-price-approval-api-call-include,planning-archive-hierarchy-audit-reliability-plan,planning-archive-hierarchy-audit-remediation,mcp-handle-chained-policy-rewrites,docs-enforce-link-validation-threshold-contract,july-july-context-briefing-reconciliation-document,audit-reconcile-current-hierarchy-evidence,deps-bump-composer-version-updates-group,deps-bump-npm-version-updates-group,auto-generate-auto-generate-planning-documentation-recovery-action,skills-imperative-declarative-refactor-skill,documentation-hierarchy-documentation-hierarchy-audit-remediation-files,refactor-persist-method-refactor-persist-method-streamline-existing,admin-wire-agent-tooling-synthetic-data -->

<!-- accomplished-unit-ids: admin-wire-agent-tooling-synthetic-data,audit-reconcile-current-hierarchy-evidence,auto-generate-auto-generate-planning-documentation-recovery-action,cta-reconcile-retry-envelope-job-type,deps-bump-composer-version-updates-group,deps-bump-npm-version-updates-group,dhar-design-system-nav,dhar-directory-index-coverage,dhar-doc-hub-refresh,dhar-frontmatter-workflow-command,dhar-link-autofix-batch,dhar-link-manual-triage,dhar-link-validation-policy,dhar-mkdocs-nav-ledger,dhar-mkdocs-nav-repair,dhar-user-facing-placeholders,dharl-current-state-reconciliation,dharl-enforced-link-mode-plan,dharl-finding-ledger-reset,dharl-link-validation-baseline,dharl-memory-path-contract,dharl-quality-gates-closeout,docs-enforce-link-validation-threshold-contract,documentation-complete-hierarchy-audit-remediation,documentation-hierarchy-documentation-hierarchy-audit-remediation-files,health-keep-idle-workers-ready,july-july-context-briefing-reconciliation-document,mcp-handle-chained-policy-rewrites,planning-archive-hierarchy-audit-reliability-plan,planning-archive-hierarchy-audit-remediation,price-approval-price-approval-api-call-include,refactor-persist-method-refactor-persist-method-streamline-existing,skills-imperative-declarative-refactor-skill -->
<!-- SECTION: ACCOMPLISHED END -->
<!-- Generated by dev-tracker build_today_plan.py -->
