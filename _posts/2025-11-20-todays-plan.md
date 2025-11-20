# Daily Plan - 2025-11-20

## Too Much

*This is entirely too much. I'm going to pare this down to a map of what is the low hanging fruit based on priorities and not a blow by blow on an hourly basis. I'll let this roll until after Thanksgiving but this structure must change.*

## Summary
- **Total items planned**: 5 focus areas
- **Estimated effort**: 7-8 hours (realistic full workday)
- **Focus areas**: 
  - Complete efficiency-metrics-refactor (near completion)
  - Advance phpunit-test-discovery Phase 2
  - Push forward product documentation reorganization
  - Progress location-based-user-flow implementation
  - Start adr-cleanup Priority 1 work

## Strategic Approach

**Philosophy**: Focus on momentum and completion. Prioritize items near the finish line to create wins, then advance in-progress work with clear next steps.

**Risk Mitigation**: Buffer time built into each block (20% capacity reserve). If blockers arise, pivot to alternative items within the same block.

---

## Morning Block (09:00-12:00) - Deep Focus Work

**Allocated Time**: 3 hours  
**Buffer**: 36 minutes (20%)  
**Net Work Time**: 2h 24min

### 1. Complete: efficiency-metrics-refactor (PRIORITY: Finish Line)

**Priority**: HIGH (88.7% complete - finish it!)  
**Effort**: 1.5 hours  
**Context**: This refactor is nearly complete with only 7 tasks remaining in cleanup and documentation phases.

**Incomplete Tasks**:

**Phase 5: Cleanup and Documentation** (3 tasks, ~45 min)
- [ ] Verify no remaining references to `CalculateEfficiencyMetricsTask`
  - Search codebase for class name references
  - Check imports, comments, documentation
- [ ] Remove `app/Containers/Core/Billing/Tasks/CalculateEfficiencyMetricsTask.php`
  - Delete the old task file
  - Run git status to confirm
- [ ] Update any remaining documentation references
  - Check CHANGELOG.md, ADRs, README files
  - Update any inline documentation

**Phase 6: Future Enhancement Preparation** (3 tasks, ~45 min - DEFERRED)
- [ ] Design ResourceAllocation migration *(Mark as deferred)*
- [ ] Plan integration with `CalculateResourceBaselinesTask` *(Mark as deferred)*
- [ ] Create interface for baseline calculation strategies *(Mark as deferred)*

**Success Criteria**:
- ✅ No code references to old task class
- ✅ Old task file removed from codebase
- ✅ Documentation updated
- ✅ Phase 6 tasks formally marked as deferred with rationale
- ✅ Checklist updated to 100% or marked complete

**Files to Review**:
- `docs/work/planning/efficiency-metrics-refactor/implementation-checklist.md`
- `app/Containers/Core/Billing/Tasks/` (for file removal)
- `CHANGELOG.md`, relevant ADRs

---

### 2. Progress: phpunit-test-discovery Phase 2 (PRIORITY: Automation)

**Priority**: MEDIUM (20.5% complete - gain momentum)  
**Effort**: 1.5 hours  
**Context**: Phase 2 focuses on automation rollout. This is currently PENDING but ready to start.

**Target Tasks** (Phase 2: Automation Rollout - select 5-6 tasks):

1. [ ] **Add post-autoload-dump hook** (~15 min)
   - Edit `laravel-app/composer.json`
   - Add hook: `"post-autoload-dump": ["@php scripts/sync-phpunit-tests.php"]`

2. [ ] **Test hook on composer install** (~10 min)
   - Run: `cd laravel-app && composer install`
   - Verify script executes automatically
   - Check output for sync confirmation

3. [ ] **Test hook on composer update** (~10 min)
   - Run: `cd laravel-app && composer update --dry-run`
   - Verify hook behavior

4. [ ] **Verify hook doesn't break workflows** (~15 min)
   - Test CI/CD compatibility
   - Check for any error output
   - Validate no side effects

5. [ ] **Run sync script manually** (~10 min)
   - Execute: `php scripts/sync-phpunit-tests.php`
   - Review output for discovered tests
   - Verify phpunit.xml updates

6. [ ] **Document automation setup** (~20 min)
   - Update README in phpunit-test-discovery planning directory
   - Add troubleshooting guide
   - Document hook behavior

**Success Criteria**:
- ✅ Composer hook added and tested
- ✅ Sync script runs on composer install/update
- ✅ phpunit.xml auto-updates with new tests
- ✅ Documentation reflects automation setup
- ✅ 6 new tasks marked complete (raises completion to ~28%)

**Files to Review**:
- `docs/work/planning/phpunit-test-discovery/implementation-checklist.md`
- `laravel-app/composer.json`
- `scripts/sync-phpunit-tests.php`

---

## Afternoon Block (13:00-17:00) - Collaborative & Implementation Work

**Allocated Time**: 4 hours  
**Buffer**: 48 minutes (20%)  
**Net Work Time**: 3h 12min

### 3. Progress: product Documentation Reorganization (PRIORITY: Planning)

**Priority**: MEDIUM (2% complete - need structure)  
**Effort**: 1.5 hours  
**Context**: Phase 1 focuses on planning the reorganization of baseline PRDs and roadmap documents.

**Target Tasks** (Phase 1: Planning & Setup - complete 4-5 tasks):

1. [ ] **Review ticket-details.md** (~20 min)
   - Read: `docs/work/planning/product/ticket-details.md`
   - Confirm classification of prd_01-07 artifacts
   - Note any roadmap/** artifacts mentioned

2. [ ] **Decide final target for baseline PRDs** (~30 min)
   - Option A: `docs/architecture/domains/product/baseline-prds/`
   - Option B: `docs/_archives/2025/product/baseline-prds/`
   - Rationale: Are these living architecture docs or historical artifacts?
   - **Decision**: Document choice in planning directory

3. [ ] **Decide final target for roadmap/process docs** (~20 min)
   - Option A: `docs/_archives/2025/archived/product-roadmap/`
   - Option B: Keep in `docs/work/planning/product/`
   - **Decision**: Document choice

4. [ ] **Identify inbound links to PRD/roadmap files** (~30 min)
   - Search across `docs/**` for references
   - Create link inventory: `product-links-inventory.md`
   - Note which files need updates after move

5. [ ] **Create feature branch** (~10 min)
   - Branch name: `feature/product-docs-reorg`
   - Base: `develop`
   - Document in planning README

**Success Criteria**:
- ✅ Classification of all PRD artifacts confirmed
- ✅ Target directories decided and documented
- ✅ Link inventory created
- ✅ Feature branch ready for work
- ✅ 4-5 tasks marked complete (~12% completion)

**Files to Review**:
- `docs/work/planning/product/ticket-details.md`
- `docs/work/planning/product/implementation-checklist.md`
- `artifacts/prd_01–07.md` files

---

### 4. Progress: location-based-user-flow Implementation (PRIORITY: Architecture)

**Priority**: MEDIUM (19% complete - continue momentum)  
**Effort**: 1.0 hour  
**Context**: Phase 1 planning tasks and Phase 2 backend work. Many tasks marked as "not needed" but need formal resolution.

**Target Tasks** (Phase 1 & 2 - resolve 4-5 tasks):

**Phase 1: Planning & Setup**
1. [ ] **Create ADR for middleware-based approach** (~30 min)
   - Document: Why middleware vs controller-based
   - Title: "ADR-00XX: Location-Based User Flow via Middleware"
   - Cover: Rationale, alternatives, consequences
   - Reference: Existing middleware implementation

2. [ ] **Design UI/UX mockups** (~20 min)
   - Sketch: Location prompt flow
   - Sketch: Location selection interface
   - Note: Defer full mockups to frontend phase
   - Document in planning directory

**Phase 2: Backend Implementation** (Resolve "not needed" tasks)
3. [ ] **Mark "not needed" tasks complete with rationale** (~10 min)
   - Update checklist: Strike through or mark complete
   - Add note: "*(Not needed - middleware-based implementation)*"
   - Clean up task list for clarity

**Success Criteria**:
- ✅ ADR created documenting middleware approach
- ✅ Basic UI flow sketched
- ✅ "Not needed" tasks formally resolved
- ✅ 3-4 tasks marked complete (~22% completion)

**Files to Review**:
- `docs/work/planning/location-based-user-flow/implementation-checklist.md`
- `docs/architecture/decisions/` (for new ADR)

---

### 5. Start: adr-cleanup Priority 1 Work (PRIORITY: Documentation)

**Priority**: MEDIUM (3.4% complete - fresh start)  
**Effort**: 0.75 hours  
**Context**: Phase 2 Priority 1 focuses on 3 ADRs with active TODO markers. This is high-value documentation work.

**Target Tasks** (Phase 2: Priority 1 - start first ADR):

**ADR-0030: First Priority 1 ADR**
1. [ ] **Read ADR-0030 in full** (~15 min)
   - Read: `docs/architecture/decisions/adr-0030-*.md`
   - Identify TODO markers
   - Understand context and intent

2. [ ] **Assess TODO markers** (~20 min)
   - Determine: Active work vs obsolete note
   - Check: Is work already completed?
   - Document findings

3. [ ] **Create implementation plan OR remove TODO** (~20 min)
   - **If active**: Create `docs/work/planning/html-debug-id/` (or relevant name)
   - **If obsolete**: Remove TODO marker
   - **If complete**: Document completion date and reference

**Success Criteria**:
- ✅ ADR-0030 analyzed
- ✅ TODO markers resolved (implementation plan created OR removed)
- ✅ ADR updated with cross-references or cleanup
- ✅ 3 tasks marked complete (~4% completion)

**Files to Review**:
- `docs/work/planning/adr-cleanup/implementation-checklist.md`
- `docs/architecture/decisions/adr-0030-*.md`

---

## Evening Block (Optional) - Low-Priority Tasks

**Allocated Time**: 1-2 hours  
**Focus**: Documentation, light planning, reflection

### Optional Tasks (Choose 1-2)

1. **Update daily plan retrospective**
   - Document what worked well
   - Note blockers encountered
   - Update planning-data.json completion percentages

2. **Review planning items in "planning" status**
   - Pick 1-2 items for next day
   - Read existing docs
   - Draft initial approach

3. **Documentation polish**
   - Review CHANGELOG.md for missing entries
   - Update README files
   - Clean up stale TODO comments

---

## Risk Mitigation

### Potential Blockers

1. **efficiency-metrics-refactor**: 
   - **Risk**: Unexpected references to old task class
   - **Mitigation**: Use comprehensive grep search; check git history for usage patterns
   - **Fallback**: Document findings, mark as "needs review" if uncertain

2. **phpunit-test-discovery**:
   - **Risk**: Composer hook breaks existing workflows
   - **Mitigation**: Test in isolation first; use dry-run flags
   - **Fallback**: Implement manual sync documentation as interim solution

3. **product**:
   - **Risk**: Unclear decision authority for directory structure
   - **Mitigation**: Document multiple options with pros/cons; defer to team discussion
   - **Fallback**: Create branch with Option A, note decision needed in PR

4. **location-based-user-flow**:
   - **Risk**: ADR numbering conflicts
   - **Mitigation**: Check latest ADR number before creating new one
   - **Fallback**: Use placeholder number, update after team review

5. **adr-cleanup**:
   - **Risk**: TODO context unclear or spans multiple concerns
   - **Mitigation**: Document uncertainty; mark for team discussion
   - **Fallback**: Move to next ADR in priority list

### Time Management

- **Buffer allocation**: 20% per block = ~1.4 hours total buffer
- **Context switching**: 10 min between major items
- **Breaks**: Pomodoro recommended (25min work / 5min break)

### Success Metrics

**Daily Goals** (realistic targets):
- ✅ Complete 1 planning item (efficiency-metrics-refactor)
- ✅ Advance 3-4 items by 5-10% each
- ✅ Mark 20-25 tasks complete across all items
- ✅ Create 1 ADR or planning document
- ✅ No blockers unresolved

---

## Notes

### Context & Assumptions

1. **All items are "medium" priority**: No critical/high priority items in dataset. Prioritization based on completion percentage and momentum.

2. **Task effort estimates**: Assuming 15 min average per task. Actual time may vary based on complexity.

3. **Planning items vs execution**: Heavy focus on documentation and planning tasks today. Future days should balance with implementation.

4. **Blocked items excluded**: `email-system-future-phases` is blocked and excluded from plan.

### Dependencies

- **efficiency-metrics-refactor → phpunit-test-discovery**: Both involve testing infrastructure; knowledge transfer potential
- **product → adr-cleanup**: Both are documentation-heavy; similar cognitive load
- **location-based-user-flow**: Independent; can be worked on anytime

### Follow-Up for Tomorrow

**Items to prioritize on 2025-11-21**:
1. Continue **phpunit-test-discovery** Phase 2 (target: 40% completion)
2. Start **product** Phase 2 (baseline PRD relocation)
3. Advance **location-based-user-flow** to frontend phase
4. Complete **adr-cleanup** Priority 1 ADRs (2 remaining)

**New items to consider**:
- **unified-build-health-dashboard** (1.2% complete, Phase 0 planning)
- **woocommerce** (5.6% complete, Phase 0 testing foundation)

---

## Appendix: Quick Reference

### Key Commands

```bash
# Efficiency Metrics Refactor
grep -r "CalculateEfficiencyMetricsTask" laravel-app/
git rm app/Containers/Core/Billing/Tasks/CalculateEfficiencyMetricsTask.php

# PHPUnit Test Discovery
cd laravel-app && composer install
php scripts/sync-phpunit-tests.php
php scripts/sync-phpunit-tests.php --dry-run

# Product Docs
git checkout -b feature/product-docs-reorg
grep -r "prd_0[1-7]" docs/
grep -r "roadmap" docs/

# Location Flow
ls docs/architecture/decisions/adr-*.md | sort | tail -1
code docs/architecture/decisions/adr-00XX-location-middleware.md

# ADR Cleanup
cat docs/architecture/decisions/adr-0030-*.md
grep -n "TODO" docs/architecture/decisions/adr-0030-*.md
```

### File Paths

- Checklists: `docs/work/planning/{item-name}/implementation-checklist.md`
- Planning data: `.daily-plans/planning-data.json`
- ADRs: `docs/architecture/decisions/`
- PRDs: `artifacts/prd_*.md`

---

**Generated**: 2025-11-20 08:00:00 UTC  
**Reviewed**: [ ] Ready for execution  
**Notes**: Focus on completion and momentum. Realistic 8-hour plan with built-in buffer.
