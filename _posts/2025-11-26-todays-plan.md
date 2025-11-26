# Daily Plan - Wednesday, November 26, 2025

**Focus:** CDP/CRM completion verification, security hardening, technical debt cleanup

---

## CDP/CRM Unified

- [ ] Run quality gates verification for Phase 2 completion (PHPStan, ESLint, TypeScript, a11y)
- [ ] Update planning status to reflect Phase 2 completion
- [ ] Review Phase 4 plan (Field Mapping UI) and identify first sprint tasks

## Security Hardening

- [ ] Change `APP_DEBUG=true` to `APP_DEBUG=false` in .env.example
- [ ] Add warning comment: `# WARNING: Set to true ONLY in local development`
- [ ] Verify APP_DEBUG default in config/app.php is `false`
- [ ] Change `PASSWORD_REQUIRE_*` defaults from `false` to `true` in .env.example

## Technical Debt

- [ ] **URGENT:** Review AbstractSyncAdapter.php:271 - migration deadline passed Nov 13
- [ ] Run grep to inventory all PHP/frontend TODOs
- [ ] Update TODO-INVENTORY.md with current counts
- [ ] Categorize TODOs by container

## ADR Cleanup

- [ ] Read ADR-0030 and assess TODO marker (active work vs obsolete)
- [ ] If active: create implementation plan in `docs/work/planning/html-debug-id/`
- [ ] If obsolete: remove TODO marker from ADR

## Database Upgrade

- [ ] Verify Docker uses MySQL 8.0+ in docker-compose.yml
- [ ] Verify Laravel database config supports MySQL 8.0 strict modes
- [ ] Audit partitioning migration for MariaDB exclusion logic

---

**Deferred:**
- WooCommerce (large scope - 458 tasks)
- CI reorganization (needs dedicated planning)
- Location-based user flow (lower priority)

**Blocked:**
- Phase 3 CRM OAuth testing (waiting on API credentials)
