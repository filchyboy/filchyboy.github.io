---
layout: post
title: "Daily Dev Log - 2026-07-26"
date: 2026-07-26
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-07-26T14:19:41.122805+00:00 -->

## Today's Plan

Sunday, and the board looks different from any point this week — yesterday was an enormous sweep through vertical slices and horizontal work that cleared dozens of feature sets simultaneously. What's left standing are two remediation tracks that have been running in the background the whole time, neither of which I've actually executed deeply. Today I close that gap.

### Main Focus

**Execute `phpstan-ratchet-knowledge-cutoff-implement` — passing effective time, knowledge cutoff, and jurisdictions correctly.** I touched this feature set yesterday and it's been active all week. The knowledge cutoff work is the implementation unit that follows the spike (`phpstan-ratchet-knowledge-cutoff-spike`, also in the ready queue), but I want to run them in order: spike first to settle the outbound-admission policy, then implement. The risk here is subtle — if I implement without locking the policy, I might pass values that are technically valid PHP but semantically wrong for the admission contract. The PHPStan ledger shows 105 errors at level 9 with only 1 of 22 units complete, so there's real distance to cover. This unit moves the needle on error count directly.

**Resolve `phpstan-ratchet-mcp-idempotency-spike` and sequence into `phpstan-ratchet-mcp-idempotency-implement`.** The MCP domain-transfer idempotency contract is the kind of problem that benefits from doing the spike and the implementation in the same session rather than splitting them across days. The spike defines what "durable idempotency key" means at the contract boundary; the implement unit actually passes that key through. Splitting them artificially creates a situation where I've decided the contract but haven't frozen it in code — and that gap tends to accumulate confusion as the surrounding code evolves. I'm genuinely uncertain whether the correct layer for idempotency enforcement is at the action class or the MCP transport boundary. That's the spike question. The implement follows from whatever the spike concludes.

**Work through `phpstan-ratchet-principal-key-narrow` and `phpstan-ratchet-scope-audit-key`.** These two are about key type narrowing — authenticated privacy principal keys and tenant-scope audit deduplication values. I've looked at these before and the issue is that both are typed too broadly somewhere in the call chain, causing PHPStan level 9 to flag possible null or union-type values where the callers expect a specific string shape. The narrowing fix has a predictable structure: find where the key is first resolved, add an explicit type assertion or early return, then let the narrowed type flow through. My concern with doing these back-to-back is that they touch adjacent domains (privacy principal resolution and audit scope) — I want to grep the audit scope deduplication first to confirm it's not drawing from the same resolution path as the principal key. If they share an ancestor, one fix might satisfy both.

**Advance `jestcov-batch-preflight` — reconciling report, ledger, and scheduled-run state.** The Jest coverage remediation plan has been active this week and I've been investing time in it, but it's still at 0 of 12 units complete with implementation not yet started. The preflight unit is the literal gate: the scheduled reviews run Monday, Wednesday, and Friday at 9 AM Pacific, which means tomorrow morning there's a scheduled pass. If I go into that run with the ledger and the 3,818-file coverage report out of sync, the batch work starts with a false baseline. The cost of doing this wrong compounds — every subsequent coverage unit in the plan would be measuring delta against an incoherent starting point.

### Secondary Work

**`phpstan-ratchet-api-tenant-route-closure` — remove instance access from the static tenant route closure.** If the key-narrowing work clears faster than expected, this is the natural continuation. It's a bounded refactor: identify what instance members the closure captures, extract those values before the closure boundary, and pass them as explicit captured variables. The question I want to answer before committing this: are there sibling closures in the tenant route setup with the same pattern? Fixing one occurrence while leaving three identical violations next to it produces a misleading ledger. A grep pass before calling it done is non-negotiable.

### Maintenance

**Run `make sync-routes` to refresh the route health report.** The current snapshot is 29 days old. With 3,447 routes tracked and active feature work landing continuously this week, that report is almost certainly misrepresenting reality. This is a single command and the output is immediately useful as a sanity check on whether yesterday's slice merges introduced any routing anomalies.

**Draft the implementation plan for `tv604-contract-scope-baseline` — the Domain Governance Live Provider Execution Loop.** The `thin-vslice-604-domain-governance-live-provider-execution-loop` plan is ready for implementation with 8 units and 0 done, and the contract baseline is the first unit. This is aligned with the governance and registry work that's been running as a theme this week (the registry-governance unified nav manifest slice is also queued). Drafting the baseline contract now means the backend orchestration and API hardening units have a defined target when I return to this plan — the contract doesn't need to be perfect, but it needs to exist.

**Address the 39 Markdownlint issues in the affected file.** The lint report shows 39 issues concentrated in a single file. If that file is in one of the planning directories I'm already touching today — `phpstan-report-ratchet-remediation` or `jest-coverage-report-ratchet-remediation` — it's worth clearing inline. If it's elsewhere, I'll identify the file first before committing to the fix.

**Scan the `phpstan-report-ratchet-remediation` planning directory for any documentation drift after yesterday's `phpstan-ratchet-test-base-concern` completion.** The plan updated its last-modified date on July 22, but that unit landed yesterday. The ledger status in the README should reflect 1/22 complete — if the frontmatter hasn't been updated, the Active Plan Status report will continue showing stale data at every planning refresh.

### Parked

The `rd100v2-state-effects-warnings-wave` work (clearing 321 ESLint State & Effects warnings outside Phase 1 hotspots) is parked today. The ESLint report shows 7,265 warnings with 5,253 marked fixable, and the State & Effects category is a meaningful subset — but tackling it requires a contiguous session focused entirely on React component patterns, which competes directly with the PHPStan type-safety work I want to close out first. Once the PHPStan ledger has more units cleared, I'll have a cleaner picture of whether any of the ESLint warnings are downstream of the same type issues.

The `deepsec-run14-external-evidence-follow-up` work (backup, IAM, external evidence reconciliation) isn't in today's plan because the PHPStan and Jest tracks are higher leverage right now. The deepsec work is ready to start but has no time-pressure forcing it ahead of the remediation tracks.

<!-- plan-unit-ids: jestcov-batch-preflight,phpstan-ratchet-api-tenant-route-closure,phpstan-ratchet-mcp-idempotency-spike,phpstan-ratchet-scope-audit-key,rd100v2-state-effects-warnings-wave -->
<!-- SECTION: DAILY-PLAN END -->

<!-- Generated by dev-tracker build_today_plan.py -->
