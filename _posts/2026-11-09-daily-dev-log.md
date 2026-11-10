---
layout: post
title: "Daily Dev Log - 2026-11-09"
date: 2026-11-09
categories: [daily, build-in-public]
tags: [dev-tracker]
---

<!-- SECTION: DAILY-PLAN START -->
<!-- publication-digest: 7b7c3210bad2cde240e947dc13319bdc3b6e68a14fe1bbdb9eadfbc4e984cd02 -->
<!-- publication-revision: 69d4d45c30e2431c9fe4b9b8b1bcec77 -->
<!-- plan-generated: 2026-11-09T14:22:31.235460+00:00 -->

## Today's Plan

Monday. The `asie-mac-mini-private-functional-completion` item finally closed yesterday — Christopher gave F7 final acceptance for F1–F3, F5, and F6, and the receipt merged. That's not nothing. What comes next in that set is genuinely different work: `asie-evidence-redaction-cleanup` and `asie-bootstrap-residual-dispositions` are about what survives into the published record versus what stays internal, not about deployment execution. The state machine remediation set also had activity in the last 24 hours — six in-progress items covering gate reviews and acceptance evidence across notice, appointment replay, and agent/browser integration.

The Shopify bulk operation readiness plan has been getting heavy attention this week. `shop-bulk-003` (verify required bulk-query access) and `shop-bulk-023` (review release evidence and canary scope) are what remain. The access verification is a provider compatibility prerequisite — it's the kind of gate that can silently block downstream work if it slips.

One thing worth naming directly: the React quality work (`rd100v2-state-effects-warnings-wave` and `rd100v2-a11y-tail-wave`) has had heavy focus this week, but the numbers are daunting enough — 321 state/effects warnings and roughly 696 accessibility warnings — that it's easy to treat the work as background rather than targeted. That's backwards. The accessibility tail in particular should have a concrete file-level target today, not just a direction.

### Main Focus

**Close `asie-evidence-redaction-cleanup` and `asie-bootstrap-residual-dispositions`.** The deployment receipt landed yesterday. These two items are what unblock `asie-reviewed-receipt-closeout`, which is the final step before the staging evidence plan archives. The redaction cleanup question is specific: which artifacts from the `dagger-disposable-lab-admission/` chain are internal deployment evidence versus what belongs in the published staging receipt. That scope boundary has been deferred for sessions but is now the only remaining authorship decision in this feature set. `asie-bootstrap-residual-dispositions` requires publishing five-class residual dispositions — this is documentation work with a known structure, and sequencing it after the redaction decision is correct because the disposition categories depend on what's in scope for the published receipt.

**Advance `sma-integrated-acceptance-notice`, `sma-integrated-acceptance-appointment-replay`, and `sma-integrated-acceptance-agent-browser`.** These three items are in the Ready to Start section of the state machine remediation set, and all three are acceptance receipt reviews — not implementation. The remediation plan decomposes into atomic gate reviews precisely so they can run in sequence without interference. Gate acceptance evidence for the delivery owner, appointment replay, and agent/browser operational integration are independent chains; none of them block each other, so I can move across all three in a single session. The risk here is that skipping them creates a gap in the integrated acceptance matrix that `sma-integrated-acceptance-matrix` depends on.

**Target a concrete file range in `rd100v2-a11y-tail-wave`.** The accessibility tail is roughly 696 warnings. Working it as an undifferentiated mass produces noise, not progress. The right move is picking a file cluster — probably the admin workspace components that the privacy category management work has been touching — and working through the specific axe-core violations there. This is where the React doctor work and the privacy category UI items have natural overlap: `col-6038-admin-style` and `col-6038-activation-ui` are both in-progress items that live in the same surface. Fixing accessibility violations in components I'm already modifying is surgical, not broad.

**Move `shop-bulk-003` to completion.** Access verification for Shopify bulk queries is a provider compatibility gate. If the required bulk-query access isn't confirmed, `shop-bulk-023` (the release evidence review) can't be scoped correctly. The plan started two days ago and sits at zero tasks complete — this needs forward movement before the week produces any outbound Shopify dependency assumptions.

### Secondary Work

**Start `sobr-journeys-remaining-1`.** The surface ownership baseline remediation had activity in the last 24 hours. Adding route journeys for the remaining admin MFE wave 1 entries is a contained task — the check script at `scripts/check_surface_ownership.py` gives immediate feedback, and the baseline is already down to 175 entries from 398. Wave 1 completion is what enables the subsequent waves to be scoped.

### Maintenance

**Regenerate PHP test results with `make test-fixed-batches-quick`.** The current test report is 102 days old, which means it's not telling me anything useful. The 1,583 failures reported may have shifted significantly — environment fixes, refactors, and dependency updates over three months could have changed the picture entirely. I can't make good decisions about PHP test health without a current baseline.

**Regenerate the TODO inventory.** The TODO inventory is 110 days old (`make todo-cleanup` or the equivalent script). After the volume of work in the last week — multiple slices closing, staging evidence landing, state machine gate reviews starting — there are almost certainly stale TODO entries pointing at resolved work.

**Review Markdownlint issues in files touched by the state machine remediation work.** There are 61 issues across 4 files. The remediation plan artifacts in `docs/work/planning/platform-state-machine-remediation-20261016/` are being actively written, so this is a reasonable time to check whether the markdown issues are concentrated there and address them in place.

**Draft the implementation plan for `migration-safety-schema-guards`.** This is flagged as aligned with active work, and the planning directory needs a plan. The connection is through safety artifacts and migration guard audit. With the state machine remediation work actively running, the guard patterns that show up there are directly relevant to what `migration-safety-schema-guards` will need to specify. Getting the plan drafted now means I can move it to Ready when the remediation gate work settles.

### Parked

**`appointment-gap-closure`** — 54 items and no recent activity. There's real work here, but it doesn't have a clear unblocking path today. The confirmation admission and expiry disposition items (`agc-01-confirm-admission`, `agc-01-expiry-disposition`) are well-defined, but starting this thread while the staging evidence closeout is still open would split attention across too many acceptance chains at once.

**`external-agent-surface-preconditions`** — Active this week but not touched in the last 24 hours. The principal model (`esp-principal-model`) and consent parity checklist (`esp-consent-parity`) need sustained attention, not a brief visit. I'll return to this when the staging evidence set archives and I have a clean slate.

**`browser-experience-closeout`** — 66 items with no recent activity. The domain governance and receipts journeys there are substantial; the right entry point is `bec-domain-governance-read-contract-create`, which creates the browser contracts through existing owner APIs. That's a good candidate for later this week once the current acceptance chains clear.

**Blocked items in `agent-auth-audit-remedation`** — `aa-decision-reconcile`, `aa-decision-revocation`, `aa-audit-envelope`, and `aa-test-audit-envelope` remain blocked. No dependency has resolved on those; parking them is the only honest call.

<!-- plan-unit-ids: col-6038-baseline-definitions,col-6038-determination-model,col-6038-scheme-migration,idr-20260728-characterization,sma-integrated-acceptance-finance,sma-integrated-acceptance-support,sma-support-gate-gate-one -->
<!-- SECTION: DAILY-PLAN END -->


<!-- SECTION: ACCOMPLISHED START -->
<!-- publication-digest: 658a846d85fac414bb2bfcce87ff3ec38cb99a91fe59dddf3870daf6d57b2d3d -->
<!-- publication-revision: d0e57af0a31f4c5d8fb660bacd6751f3 -->
<!-- accomplished-generated: 2026-11-10T03:33:49.485692+00:00 -->

## Today's Update

Today was dominated by two substantial feature areas that share almost no code but do share a design principle: when the system doesn't know what to do, it should refuse rather than guess. That showed up in the compliance masking work and again in the privacy category scheme work, in different forms but with the same intent.

The compliance feature set was the larger body of work by a wide margin — roughly 28 items across the `DataMaskingService` and the surrounding masking infrastructure. The through-line was building a masking layer that fails closed at every ambiguous boundary rather than silently passing data through. I started by implementing lazy loading for masking rules, so the service only pays the I/O cost on first use rather than at boot. From there, the work expanded outward in a methodical way: refuse field-type mappings that name a missing strategy, fail closed when the masking rule directory is missing, fail closed when no mapped strategy can handle a given field type, fail closed for values in a list with no name. Each of those is a distinct failure mode that needed its own test path.

The more structurally interesting compliance work was around field matching and collection traversal. Getting `DataMaskingService` to correctly mask nested response fields under their own names, handle numeric-key JSON objects without converting them to arrays, and match camelCase and other-case field names to snake_case taxonomy entries — that's the part where the edge cases actually accumulate. I added an alias mechanism for fields named in other languages, and I'm not fully settled on whether the alias list belongs in the taxonomy or as a separate config file. Right now it's in taxonomy, which keeps lookup logic in one place, but it means the taxonomy file grows with every localization concern added. I'll likely revisit that boundary when the taxonomy gets its first real-world exercise. The COPPA-specific work — masking `parental_email` for every viewer outside consent scope, and correctly resolving `parent_email` as an alias for `parental_email` — required its own taxonomy entries for `ssn` and `tax_id` as well. Those weren't there before, and without them the masking middleware was quietly passing those field values through for roles that shouldn't see them. That's exactly the kind of silent gap the fail-closed policy is meant to prevent.

The privacy category management work is a foundation layer: `PrivacyCategoryScheme` model, its migration for scheme identity and version persistence, a provenance-linked baseline vocabulary, and the read UI that presents tenant vocabulary alongside remediation gaps. The comparison logic for detecting material determination changes is the piece I want to revisit — it works for the cases I've defined, but "material" is doing a lot of work there and the threshold for what counts as a material change versus a cosmetic one isn't formally specified yet. That ambiguity is fine right now because there are no tenant environments exercising it, but it will need a crisper definition before the scheme versioning logic is exposed to any real operator workflow. The thin vertical slice work (tv703) covered the full progression for the breaking required-field approval loop: contract scope baseline, backend orchestration, data determinism, API contract hardening, React frontend integration, observability instrumentation, quality gates, and focused accessibility tests. That's a complete slice, archived.

The remaining items — `record-scheme-publisher` decisions around publisher account and no-fallback handling, the support system's isolated Case and Ticket compatibility enforcement, and a tracker commit bundling the MySQL permission and npm guard work from yesterday's runtime session — are smaller in scope but each closes a gap that would otherwise require a decision at runtime. Recording the no-fallback decision for scheme publishers now means that path has a documented stance rather than an implicit one. The MySQL role hierarchy qualification tasks went into the tracker as new support work; that's setup for future profile definition writers who need to understand what the permission boundaries are before they write against them.

<!-- accomplished-unit-ids: col-6038-baseline-definitions,col-6038-determination-compare,col-6038-determination-review,col-6038-scheme-migration,col-6038-scheme-model,col-6038-tenant-read-ui,compliance-apply-custom-masking-rules-fields,compliance-bring-config-compliance-masking-php-repo-s-pint-rules,compliance-clarify-selected-scheme-publisher-role,compliance-cover-top-level-list-scalars-through,compliance-fail-closed-unreadable-masking-rule,compliance-fail-closed-values-list-with,compliance-fail-closed-when-mapped-strategy,compliance-fail-closed-when-masking-rule,compliance-fail-closed-when-masking-rules,compliance-give-email-phone-taxonomy-entries,compliance-give-ssn-tax-id-taxonomy-entries,compliance-keep-json-objects-with-numeric,compliance-load-datamaskingservice-masking-rules-first,compliance-mask-fields-named-other-languages,compliance-mask-list-items-under-list,compliance-mask-named-map-keys-under,compliance-mask-nested-response-fields-under,compliance-mask-numeric-key-objects-under-their,compliance-mask-parent-email-parental-email,compliance-mask-parental-email-every-viewer-outside,compliance-match-camelcase-other-case-fields-snake-case,compliance-match-unusually-named-lists-their,compliance-never-use-masking-rule-set,compliance-read-custom-masking-rule-groups,compliance-reconcile-p01-publisher-role-with,compliance-record-scheme-draft-fallback-decision,compliance-refuse-field-type-mappings-that-name,compliance-set-masking-context-s-user-role-from,record-scheme-publisher-record-scheme-publisher-account-no-fallback,support-enforce-isolated-case-ticket-compatibility,tracker-new-support-tasks-mysql-permission,tv703-api-contract-hardening,tv703-backend-orchestration,tv703-contract-scope-baseline,tv703-data-determinism,tv703-focused-tests-a11y,tv703-frontend-integration,tv703-observability-instrumentation,tv703-quality-gates-handoff -->
<!-- SECTION: ACCOMPLISHED END -->
