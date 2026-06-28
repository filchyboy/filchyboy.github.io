---
layout: post
title: "Daily Dev Log - 2026-06-28"
date: 2026-06-28
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-06-28T13:26:39.432794+00:00 -->

## Today's Plan

Sunday. The phpstan-baseline-remediation work is genuinely moving — two items from that plan landed as unplanned yesterday, which tells me the remediation sweep has its own gravity right now. The cryptographic-provenance-kms-productionization plan has been touched in the last 24 hours too and is ready to start. Both need attention today, and neither is blocked.

### Main Focus

**Continue the phpstan-baseline-remediation sweep, targeting `phpstan-type-shape-ship-compliance` and `phpstan-type-shape-mcp-etl`** — The remediation plan is 3/16 work units complete with 10 in progress. Yesterday I cleared `phpstan-custom-guardrail-findings` and `phpstan-test-contract-residuals` outside the plan, which means the custom guardrail surface and test residuals are already handled. The type-shape repairs in Ship, Compliance, MCP, and ETL are the highest-volume category next in sequence, and working them out of order from the runtime-shape items matters: type-shape annotations target property declarations and return types, while runtime-shape repairs target call sites. Conflating the two in a single pass produces inconsistent annotation patterns that require a second cleanup sweep — something I've burned time on before in this codebase. PHPStan is sitting at 866 errors at level 9 per the fresh snapshot today. The checkpoint evidence in the plan shows 1,317 harness files processed out of 15,593, meaning there's a lot of runway here, but the type-shape batch is the right place to be right now before the runtime-shape items in Phase 3.

**Begin the cryptographic-provenance-kms-productionization baseline work, starting with `crypto-prov-kms-source-baseline` and `crypto-prov-kms-current-surface-inventory`** — This plan is at 0/32 tracker items complete after being worked on in the last 24 hours. The plan's framing is specific: provenance owns invocation signing custody; CryptoErasure KMS patterns are references, not the invocation private-key runtime owner. That distinction matters before any contract work begins, because `crypto-prov-kms-boundary-contract` (the third item) can't define ownership accurately without the inventory showing what signing custody surfaces currently exist. The source baseline is genuinely the first step — I need to know what material the boundary contract will be drawing from before I write that contract. The plan notes the implementation trigger is enabling signed invocation verification outside local/staging, which is a production gate I don't want to open without the custody chain being explicit.

**Work through `crypto-prov-kms-boundary-contract` and `crypto-prov-kms-production-driver-contract` if the inventory clears** — These two contract definitions are sequenced for a reason: the ownership contract (`crypto-prov-kms-boundary-contract`) defines who holds signing custody, and the production driver contract (`crypto-prov-kms-production-driver-contract`) defines the interface that production `SigningKeyStore` drivers must satisfy. Writing the driver contract without the ownership contract in place is the same class of sequencing error that bit me in earlier provenance work — the driver ends up encoding ownership assumptions that the boundary contract later contradicts. If the first two items land cleanly, I can run through these two in the same session.

**Advance `phpstan-runtime-shape-compliance-mcp-etl`** — This is the runtime-shape counterpart to the type-shape work, covering Compliance, MCP, and ETL domains. It's in-progress and lives in Phase 3 of the plan. I'm listing it explicitly because the risk of leaving the runtime-shape items untouched while finishing type-shape repairs is that PHPStan's error report becomes harder to read — the two categories intermingle in the JSON output and I'll lose the signal about which domain has the most remaining errors. Getting a partial pass on the runtime-shape items today sharpens the report for tomorrow's sweep.

### Secondary Work

**Draft the `crypto-prov-kms-rotation-contract` and `crypto-prov-kms-revocation-contract` definitions** — These are later in the sequence (items 6 and 7 of 8 in the planning work), but the design questions for both are concrete: overlapping manifest rotation means deciding what the overlap window is and how custody transfers during that window, and revocation means deciding whether a revoked signing key invalidates historical signatures or only future ones. I'm genuinely uncertain which side of that trade-off is right for the platform's threat model. Getting the design question written down — even as an open question in the contract artifact — is more valuable than leaving it entirely unstarted.

### Maintenance

**Refresh the PHP test report with `make test-fixed-batches-quick`** — The test snapshot is 13 days old, showing 0/50 passed. That number is likely environment-related rather than a true 0% pass rate, but I won't know until I run a fresh pass. Thirteen days is too long to go without a current baseline, and the test surface touches several domains I've been actively modifying this week.

**Regenerate the TODO inventory** — The inventory is 12 days old with 0 items tracked, which is almost certainly wrong given the volume of code that's landed since June 16. The todo-cleanup script produces this and it's a five-minute refresh. I want an accurate number before committing to any code changes in the KMS productionization work.

**Draft the `cb-meter-source-baseline` planning artifact for context-briefing-metered-generation** — This is the first work unit in a 7-item plan at 0% complete. The plan has billing, cadence, and commerce-billing domain tags, and the source baseline exists to confirm what metering surface material is already present before any contract work begins. This is planning work I can do in parallel with the remediation sweep — it doesn't require deep implementation context, just a review of what's already in the codebase.

**Address Markdownlint issues in planning files being touched today** — The lint harness shows 175 Markdownlint issues across 11 files. The cryptographic-provenance-kms-productionization planning directory is being edited today for the contract baseline work. Fixing Markdownlint violations in files I'm already writing reduces the issue count without a broad automated sweep, and the violations in planning documents tend to be simple: missing blank lines around headings, trailing spaces, bare URLs.

### Parked

The `security-prod-boundary-sprint` (27 units, next: `security-prod-boun-1831-scope`) and `tenant-trust-cryptographic-tenant-boundaries` (13 units, next: `tenant-crypto-source-material-baseline`) are both ready to start but I'm not touching them today. The cryptographic-provenance-kms work already occupies the trust/signing custody domain for today, and splitting attention across two zero-percent plans in adjacent security domains in a single session produces shallow first passes on both rather than a solid foundation on either. `deferred-scale-certification-follow-up` is similarly ready but structurally independent — 31 units with an assessment/auditor-package scope that deserves a dedicated session, not a Sunday afternoon tag-on.

<!-- plan-unit-ids: crypto-prov-kms-source-baseline,phpstan-report-visibility-ratchet,phpstan-type-shape-ship-compliance,phpstan-type-shape-userworkflow-logging -->
<!-- SECTION: DAILY-PLAN END -->

<!-- Generated by dev-tracker build_today_plan.py -->
