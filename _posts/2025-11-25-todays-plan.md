# Daily Plan - Tuesday, November 25, 2025

**Focus Areas:** Complete trust infrastructure foundation (matches current branch COL-7803-Trust-Infra), finish unified linting command setup, and address security configuration defaults. Continue CDP scaffolding Phase 6 setup.

**Current Branch:** `COL-7803-Trust-Infra`

**Time Budget:** ~8 hours (estimated)

---

## High Priority (Blockers & Critical Path)

### 1. Trust Infrastructure - ADR Creation
**Est: 1.5hr | Priority: HIGH | Blocking: All trust implementation**

Create ADR for trust ontology and policy registry decisions. This establishes the architectural foundation for the trust infrastructure feature.

**Tasks:**
- [ ] **[Trust]**: Create ADR for trust ontology and policy registry decisions - _Why: Required foundation before any trust implementation work_
- [ ] **[Trust]**: Review architecture with team (cross-functional sign-off) - _Context: ADR needs validation_

**Files:**
- `docs/architecture/decisions/adr-XXXX-trust-ontology-policy-registry.md`

---

### 2. Trust Infrastructure - JSON Schema Design
**Est: 2hr | Priority: HIGH | Blocking: Backend models and validation**

Design the canonical JSON schemas that will define the trust domain objects.

**Tasks:**
- [ ] **[Trust]**: Design JSON schemas (`ConsentReceipt`, `ResidencyAssertion`, `MonetaryEvent`, `PolicyRecord`) - _Why: Foundation for backend models and API validation_
- [ ] **[Trust]**: Design database schema for `trust_policies` and `trust_receipt_ledger` - _Context: Follows JSON schema design_

**Files:**
- `schemas/trust/ConsentReceipt.json`
- `schemas/trust/ResidencyAssertion.json`
- `schemas/trust/MonetaryEvent.json`
- `schemas/trust/PolicyRecord.json`

---

### 3. Unified Linting Command - Composer Scripts
**Est: 30min | Priority: HIGH | Blocking: Developer workflow improvements**

Add PHP linting scripts to Laravel composer.json for unified developer experience.

**Tasks:**
- [ ] **[Unified Linting]**: Add `fix-style` script to laravel-app/composer.json - _Why: Quick win, improves dev workflow_
- [ ] **[Unified Linting]**: Add `lint:all` composite script to composer.json - _Context: Combines all PHP linters_
- [ ] **[Unified Linting]**: Test `composer fix-style` executes correctly
- [ ] **[Unified Linting]**: Test `composer lint:all` executes correctly
- [ ] **[Unified Linting]**: Verify no breaking changes to existing scripts

**Files:**
- `laravel-app/composer.json`

---

### 4. Security Configuration Defaults
**Est: 30min | Priority: HIGH | Blocking: Security compliance**

Update .env.example with secure default values for critical security settings.

**Tasks:**
- [ ] **[Secure Config]**: Change `APP_DEBUG=true` to `APP_DEBUG=false` in laravel-app/.env.example - _Why: Prevents accidental debug exposure in production_
- [ ] **[Secure Config]**: Add comment: `# WARNING: Set to true ONLY in local development`
- [ ] **[Secure Config]**: Change `PASSWORD_REQUIRE_UPPERCASE=false` to `true`
- [ ] **[Secure Config]**: Change `PASSWORD_REQUIRE_LOWERCASE=false` to `true`
- [ ] **[Secure Config]**: Change `PASSWORD_REQUIRE_NUMBERS=false` to `true`
- [ ] **[Secure Config]**: Change `PASSWORD_REQUIRE_SPECIAL_CHARS=false` to `true`
- [ ] **[Secure Config]**: Add section comment explaining password policy settings

**Files:**
- `laravel-app/.env.example`

---

## Medium Priority (Continue In-Progress Work)

### 5. CDP Scaffolding - Phase 6 Design System Setup
**Est: 1.5hr | Priority: MEDIUM | Depends on: Design tokens**

Begin Phase 6 frontend UI work by setting up the CSS Modules foundation.

**Tasks:**
- [ ] **[CDP Scaffolding]**: Verify design tokens cover CDP UI needs - _Why: Foundation for all CSS Modules_
  - Colors for provenance event types (8 types)
  - Colors for CRM platforms (HubSpot, FluentCRM)
  - Colors for connection health (healthy, degraded, failed)
- [ ] **[CDP Scaffolding]**: Create CSS Module: `frontend/src/styles/components/CDP/CDPComponents.module.scss` - _Context: Shared CDP component styles using design tokens_
- [ ] **[CDP Scaffolding]**: Validate design tokens: `make tokens-validate`
- [ ] **[CDP Scaffolding]**: Build design tokens: `make tokens-build`

**Files:**
- `frontend/src/styles/tokens/`
- `frontend/src/styles/components/CDP/CDPComponents.module.scss`

---

### 6. CRM Integration - Quality Gates
**Est: 45min | Priority: MEDIUM | Blocking: Phase 1 completion**

Run quality gate checks on CRM integration Phase 1 work.

**Tasks:**
- [ ] **[CRM Integration]**: PHPStan level 5: `make lint-php` on ETL container - _Why: Code quality gate_
- [ ] **[CRM Integration]**: All unit tests passing: `make test-filter FILTER="ETL/Tests/Unit"`
- [ ] **[CRM Integration]**: All integration tests passing: `make test-filter FILTER="ETL/Tests/Integration"`

---

## Quick Wins (Low-Hanging Fruit)

### 7. Trust Infrastructure - Environment Setup
**Est: 15min | Priority: LOW | Value: Foundation work**

- [ ] **[Trust]**: Create feature branch (if not already on COL-7803-Trust-Infra)
- [ ] **[Trust]**: Set up development environment
- [ ] **[Trust]**: Add environment variables for HMAC keys to .env.example

---

### 8. Database Upgrade - Quality Gates
**Est: 30min | Priority: LOW | Value: Infrastructure validation**

- [ ] **[Upgrade DB]**: Run PHPStan analysis: `make lint-php` - _Why: Verify database-related code quality_
- [ ] **[Upgrade DB]**: Verify Docker uses MySQL 8.0+ (`docker/docker-compose.yml`)
- [ ] **[Upgrade DB]**: Verify charset is utf8mb4 and collation is utf8mb4_unicode_ci

---

### 9. Frontend Quality Gates
**Est: 30min | Priority: LOW | Value: CI readiness**

- [ ] **[Quality Gates]**: Run ESLint: `npm run lint`
- [ ] **[Quality Gates]**: Run TypeScript checks: `npm run type-check`

---

## Deferred Items (Not Today)

The following items are explicitly deferred based on current priorities:

| Item | Reason | When |
|------|--------|------|
| **ADR Cleanup Phase 2+** | Trust infrastructure takes priority | After trust foundation |
| **WooCommerce Integration** | 458 tasks, low priority | Future sprint |
| **CDP Scaffolding Phase 6 Components** | Design system setup first | After design tokens verified |
| **Impersonation Feature** | Planning phase only | Future sprint |
| **Tailwind Migration** | Planning phase only | Future sprint |

---

## Dependencies Map

```
[Trust ADR Creation] ──────────────────┐
                                       ├──> [Trust JSON Schemas]
[Trust Environment Setup] ─────────────┘         │
                                                  ▼
                                        [Trust Backend Work]
                                              (future)

[Unified Linting Scripts] ──> [Quality Gate Improvements]

[Security Config Defaults] ──> [Security Compliance]

[CDP Design Tokens Verify] ──> [CDP CSS Modules] ──> [CDP Components]
                                                       (Phase 6)
```

---

## Success Criteria for Today

| Criteria | Target | Measurement |
|----------|--------|-------------|
| Trust ADR created | 1 ADR | ADR file exists with decision documented |
| Trust JSON schemas | 4 schemas | Schema files created with validation |
| Unified linting scripts | 2 scripts | `composer fix-style` and `composer lint:all` working |
| Security defaults | Updated | APP_DEBUG=false, PASSWORD_* defaults=true |
| PHPStan errors | 0 | `make lint-php` clean |
| ESLint errors | 0 | `npm run lint` clean |
| TypeScript errors | 0 | `npm run type-check` clean |

---

## Risks & Blockers

| Risk | Mitigation |
|------|------------|
| Trust ADR requires team review | Document decisions clearly, async review if needed |
| JSON schema validation may need new tooling | Use existing JSON Schema validator in CI |
| Security config changes may break local dev | Clear documentation in .env.example comments |

---

## Commands Reference

```bash
# Quality Gates
make lint-php                                    # PHPStan Level 5
npm run lint                                     # ESLint
npm run type-check                               # TypeScript

# Testing
make test-filter FILTER="ETL/Tests/Unit"         # ETL unit tests
make test-filter FILTER="ETL/Tests/Integration"  # ETL integration tests

# Design Tokens
make tokens-validate                             # Validate tokens
make tokens-build                                # Build tokens

# Composer Scripts (after adding)
cd laravel-app && composer fix-style             # Auto-fix PHP style
cd laravel-app && composer lint:all              # Run all PHP linters

# Git
git status                                       # Check working tree
git log --oneline -5                            # Recent commits
```

---

## Quality Rubric Scores (Top Selected Tasks)

| Task | Specificity | Actionability | Value | Avg |
|------|-------------|---------------|-------|-----|
| Trust ADR creation | 4 | 5 | 5 | 4.7 |
| Trust JSON schemas | 5 | 4 | 5 | 4.7 |
| Unified lint fix-style | 5 | 5 | 4 | 4.7 |
| Unified lint:all script | 5 | 5 | 4 | 4.7 |
| APP_DEBUG=false | 5 | 5 | 5 | 5.0 |
| Password policy defaults | 5 | 5 | 5 | 5.0 |
| CDP design tokens verify | 4 | 4 | 4 | 4.0 |
| CDP CSS Module | 5 | 5 | 4 | 4.7 |
| PHPStan analysis | 5 | 5 | 4 | 4.7 |
| ESLint/TypeScript | 5 | 5 | 4 | 4.7 |

All tasks score >= 4.0 (above minimum 3.0 threshold).

---

## Progress Tracking

| Project | Status | Tasks Today | Notes |
|---------|--------|-------------|-------|
| Trust Infrastructure | Starting | 5 tasks | Foundation work (ADR, schemas) |
| Unified Linting Command | In Progress | 5 tasks | Complete Phase 1 |
| Secure Default Config | In Progress | 7 tasks | Phase 1 completion |
| CDP Scaffolding | Phase 6 Ready | 4 tasks | Design system setup |
| CRM Integration | Quality Gates | 3 tasks | Validation checks |
| Upgrade DB | Quality Gates | 3 tasks | Infrastructure validation |

---

**Total Estimated Time:** ~7.5 hours
**Task Count:** 27 granular tasks across 9 work items (organized into 4 high, 2 medium, 3 quick wins)

---

## Recent Context

**Recent Commits:**
- `docs(trust): migrate planning documents to template-compliant format and archive originals`
- `refactor(CDP): remove unused getDisplayNameOrFallback function from ContactDetail`
- `docs: improve formatting consistency in CRM integration unified README`
- `refactor(cdp/etl): update NULL operator validation in SalesforceQueryBuilder`

**Current Focus:** Trust infrastructure aligns with branch COL-7803-Trust-Infra. CDP/CRM work continues from recent momentum.
