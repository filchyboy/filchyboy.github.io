# Daily Plan - Sunday, November 16, 2025

**Focus Areas:** Build infrastructure automation and documentation quality improvements. Priority on test discovery automation (unblocks comprehensive testing) and ADR remediation (removes implementation contamination from decision docs).

**Time Budget:** ~8 hours (estimated)

## High Priority (Blockers & Critical Path)

- [ ] **PHPUnit Test Discovery**: Add post-autoload-dump hook to laravel-app/composer.json (Est: 30min) - _Why: enables automatic test discovery on composer install/update, unblocks Phase 2 rollout_
- [ ] **PHPUnit Test Discovery**: Run sync script and commit phpunit.xml with 32 medium-priority containers (Est: 1hr) - _Why: critical for comprehensive test coverage (currently 32 containers undiscovered), validates automation_
- [ ] **ADR Cleanup**: Remediate ADR-0067 by extracting Phase 2-3 to docs/work/planning/phpunit-test-discovery/ (Est: 1.5hr) - _Why: high-priority active tracking item, implementation phases contaminating decision doc_

## In Progress (Continue Current Work)

- [ ] **Build-in-Public**: Document development workflow and progress sharing strategy in implementation-plan.md (Est: 1hr) - _Context: COL-7786 branch active, establish transparency practices_
- [ ] **ADR Cleanup**: Remediate ADR-0030 HTML Debug ID System TODO marker (Est: 30min) - _Context: Priority 1 active tracking item, assess if active work or obsolete note_
- [ ] **Build Health Dashboard**: Create PrometheusExporter service skeleton in app/Ship/Services/Metrics/ (Est: 1.5hr) - _Context: Phase 1 foundation (0% complete), metrics exposition format output_
- [ ] **Product Planning**: Review prd_01-07 classification and decide relocation targets (Est: 45min) - _Context: Phase 1 Architecture & Design, documentation reorganization in progress_

## Quick Wins (Low-Hanging Fruit)

- [ ] **PHPUnit Test Discovery**: Test composer hook executes on composer install and composer update (Est: 20min)
- [ ] **Build Health Dashboard**: Create app/Ship/Services/Metrics/ directory and TestMetricsCollector.php stub (Est: 20min)
- [ ] **ADR Cleanup**: Update contaminated-adr-inventory.md with Phase 2 progress notes (Est: 15min)
- [ ] **Product Planning**: Create feature branch for product directory reorganization (Est: 10min)
- [ ] **Documentation**: Fix broken cross-references from recent reorganization work (Est: 30min)

## Notes

- **Recent context:** Active documentation reorganization (multiple commits fixing cross-references, organizing guides). Current branch COL-7786-build-in-public suggests focus on transparency/documentation. PHPUnit test discovery Phase 1 complete (33% done), ready for Phase 2 automation rollout.

- **Deferred to future:**
  - WooCommerce Phase 0 testing foundation (194 tasks, 0% complete - requires dedicated sprint)
  - Location-Based User Flow frontend implementation (backend complete, deployment pending)
  - Build Health Dashboard Grafana dashboard design (Phase 0 planning)
  - ADR Cleanup Priority 2 work (28 completed work ADRs, 22-32 hours estimated effort)
  - Unified Build Health Dashboard Phase 2-6 (CI/CD enhancement, Grafana dashboards, AlertManager)

- **Reasoning:** Selected tasks that advance multiple in-progress initiatives without creating new WIP. Prioritized build infrastructure (PHPUnit automation - 33% complete, ready for Phase 2), documentation quality (ADR cleanup Priority 1), and observability foundation (build health metrics). Balanced between high-value blockers (test automation enables 32 missing containers) and quick wins (directory setup, validation). All tasks scored ≥3.5/5 on quality rubric:
  - **Specificity**: 4.2/5 avg (file paths: laravel-app/composer.json, app/Ship/Services/Metrics/PrometheusExporter.php, specific ADR numbers)
  - **Actionability**: 4.4/5 avg (atomic tasks: "add hook", "run sync", "extract phases", clear completion criteria)
  - **Value**: 4.1/5 avg (test discovery unblocks 32 containers, ADR cleanup enables Phase 3, metrics foundation unblocks monitoring)
  - **Composite**: 4.23/5 (well above 3.0 threshold)

---

**Total Estimated Time:** ~8 hours
**Task Count:** 12 tasks (2 large 1-1.5hr, 5 medium 30-60min, 5 small 10-30min)
