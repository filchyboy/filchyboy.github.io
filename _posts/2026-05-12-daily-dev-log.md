---
layout: post
title: "Daily Dev Log - 2026-05-12"
date: 2026-05-12
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- plan-generated: 2026-05-12T13:13:26.954359+00:00 -->

## Today's Theme

The two authorization slices I started yesterday are pulling me in different directions - tv447 needs its frontend integration to complete the freeze window workflow, while tv449 is stuck waiting for API contract hardening. But honestly, I'm most excited about finally tackling that security scan program I've been planning. The Phase 0 baseline work should reveal exactly how exposed we are, and I'd rather know the truth than keep wondering if we've got secrets bleeding in our git history.

## The Main Work

**Wire up the PublishingFreezeWindowPanel with datetime-local inputs (tv447-frontend-integration)** - I built the backend orchestration yesterday but left the React side hanging. The datetime-local input handling is going to be finicky because timezone semantics matter for publishing schedules, and I need the preview/confirm flow working before anyone can actually test this feature. Without the frontend, all that backend work is just dead code.

**Build the GET /api/v1/authorize endpoint for bulk permission checks (tv449-api-contract-hardening)** - The authorization policies I created yesterday are useless without a way for the frontend to query them efficiently. Five separate permission calls per page load is ridiculous when I can batch them into a single request. This endpoint either makes the authorization system practical or forces me to rethink the entire approach.

**Run the security sweep baseline to capture our current exposure (ssp-phase0-run-security-sweep)** - I'm genuinely nervous about what this will find. We've been sloppy about credential hygiene for years, and if there are API keys or database passwords lurking in old commits, that's a compliance disaster waiting to happen. The security-sweep.sh script either gives me peace of mind or ruins my day with emergency remediation work, but either way I need to know.

**Complete the 5 PolicyTest classes with cross-tenant validation (tv449-focused-tests-a11y)** - Testing authorization logic is where subtle bugs hide, especially around tenant boundaries. A policy that accidentally grants access across tenant boundaries isn't just a bug - it's a data breach. The jest-axe integration is secondary, but the cross-tenant test coverage is critical for production confidence.

## Housekeeping

**Regenerate the 13-day-old PHP test results with `make test-fixed-batches-quick`** - The 89% pass rate might be stale, and if I'm touching authorization code today, I want current test health before I introduce new failures.

**Draft an implementation plan for horizontal-slice-openapi-form-request-contract-parity-gate** - This aligns with the API contract work I'm doing on tv449, and the scaffolding exists but needs an actual implementation roadmap.

**Replace template boilerplate in planning directory (todoremed-p0-replace-template-boilerplate)** - This has been irritating me every time I create new planning docs. The placeholder text is worse than no text.

## Parked

The `make dev-up` CI validation from hs126 can wait - the orchestration landed yesterday and proving it works in a clean container isn't blocking anything immediate. The accidental-pint remediation cohorts are down to just two items, but they're not urgent enough to derail the authorization work that's actually in motion.

I'm also setting aside any broad PHPStan remediation today. The 3,992 errors at level 9 represent months of work, and randomly fixing a few won't meaningfully improve the codebase health.

<!-- plan-unit-ids: accidental-pint-core-etl,hs126-ci-smoke-dev-up,todoremed-p0-replace-template-boilerplate,tv447-api-contract-hardening,tv449-api-contract-hardening -->
<!-- SECTION: DAILY-PLAN END -->


<!-- SECTION: ACCOMPLISHED START -->
<!-- accomplished-generated: 2026-05-12T15:57:37.822387+00:00 -->

## Today's Update

Today was about closing loops - finishing three major vertical slices that have been running in parallel for weeks, plus hardening the platform's security posture with some overdue supply chain protections.

The three thin vertical slices (TV447, TV448, and TV449) all reached completion today, which feels significant because they represent different facets of the admin experience that needed to work together. TV447 was the publishing freeze window system - I built out the PublishingFreezeWindowPanel with datetime-local inputs and a proper preview/confirm flow. The backend orchestration was straightforward once I got the tenant-scoped queries right, but the dry-run preview logic took some thinking through. TV448 was the DSR bulk operations console, which required more complex state management because of the partial-success scenarios. The BulkDsrActionRouter dispatches to queues, but the frontend needed polling and modal states to handle operations that might succeed for some records and fail for others. TV449 was authorization policy coverage across five models - mostly plumbing work to get the useAuthorize hook adopted consistently and wire up the GET /api/v1/admin/authorize endpoint properly.

The security hygiene work was long overdue but surprisingly satisfying to complete. I ran gitleaks against the full git history, which turned up exactly the kinds of old credential fragments you'd expect in a project that's been running for two years. Added gitleaks to the pre-commit hooks and set up the GitHub workflow to run secret scanning on every PR with SARIF upload. The dependency audit workflow covers both composer and npm, running on PRs and nightly. What I hadn't anticipated was how much documentation this would require - had to create a proper exemption flow document and update the security agents doc to explain how all these tripwires work together.

The React Doctor followup sprint also wrapped up today. Getting that root score to exactly 100 took more iterations than expected - every time I fixed one bucket of diagnostics, it would reveal issues in another area. The dead code audit surfaced some interesting architectural debt, and the React 19 preparation work highlighted a few patterns we'll need to change before upgrading. I'm glad this is archived now because the constant re-measuring was getting tedious.

This sets up Monday nicely - with these three feature slices complete and the security baseline established, I can focus on the frontend admin parity work without carrying around a bunch of half-finished threads.

**The Numbers:**
- Completed: 36 tasks
- Feature areas: thin-vslice-450-admin-destructive-confirm-useauthorize-adoption, thin-vslice-447-publishing-release-datetime-freeze-window, thin-vslice-449-authorization-policy-coverage-five-models, thin-vslice-448-dsr-bulk-operations-operator-console, secret-hygiene-supply-chain-tripwires, react-doctor-100-followup-sprint


<!-- Generated by dev-tracker publish_to_jekyll.py (AI mode) -->
<!-- accomplished-date: 2026-05-12 -->
<!-- unit-ids: tv450-contract-scope-baseline,tv447-frontend-integration,tv449-frontend-integration,tv449-focused-tests-a11y,tv449-api-contract-hardening,tv448-contract-scope-baseline,tv448-backend-orchestration,tv448-frontend-integration,tv447-api-contract-hardening,tv448-focused-tests-a11y,tv449-observability-instrumentation,tv447-focused-tests-a11y,tv448-data-determinism,tv448-api-contract-hardening,tv447-quality-gates-handoff,tv449-quality-gates-handoff,tv448-observability-instrumentation,tv448-quality-gates-handoff,secret-hygiene-history-scan,secret-hygiene-env-diff,secret-hygiene-precommit-gitleaks,secret-hygiene-secret-scan-workflow,secret-hygiene-dependency-audit-workflow,secret-hygiene-exemption-doc,secret-hygiene-agents-doc-update,rd100-remeasure-root-and-frontend,rd100-finish-state-bucket-wave,rd100-finish-hydration-and-intl-wave,rd100-finish-generic-handler-wave,rd100-audit-dead-code-and-react19-buckets,rd100-close-root-score-gap,rd100-archive-sprint-plan,tv447-contract-scope-baseline,tv447-backend-orchestration,tv447-data-determinism,tv447-observability-instrumentation -->

<!-- accomplished-unit-ids: rd100-archive-sprint-plan,rd100-audit-dead-code-and-react19-buckets,rd100-close-root-score-gap,rd100-finish-generic-handler-wave,rd100-finish-hydration-and-intl-wave,rd100-finish-state-bucket-wave,rd100-remeasure-root-and-frontend,secret-hygiene-agents-doc-update,secret-hygiene-dependency-audit-workflow,secret-hygiene-env-diff,secret-hygiene-exemption-doc,secret-hygiene-history-scan,secret-hygiene-precommit-gitleaks,secret-hygiene-secret-scan-workflow,tv447-api-contract-hardening,tv447-backend-orchestration,tv447-contract-scope-baseline,tv447-data-determinism,tv447-focused-tests-a11y,tv447-frontend-integration,tv447-observability-instrumentation,tv447-quality-gates-handoff,tv448-api-contract-hardening,tv448-backend-orchestration,tv448-contract-scope-baseline,tv448-data-determinism,tv448-focused-tests-a11y,tv448-frontend-integration,tv448-observability-instrumentation,tv448-quality-gates-handoff,tv449-api-contract-hardening,tv449-focused-tests-a11y,tv449-frontend-integration,tv449-observability-instrumentation,tv449-quality-gates-handoff,tv450-contract-scope-baseline -->
<!-- SECTION: ACCOMPLISHED END -->
<!-- Generated by dev-tracker build_today_plan.py -->
