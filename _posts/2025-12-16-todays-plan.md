---
layout: post
title: "Daily Plan - 2025-12-16"
date: 2025-12-16
---

# Daily Plan - Tuesday, December 16, 2025

## Today's Theme
I'm focusing on foundational infrastructure today - the unglamorous but essential work that makes everything else easier. I've got a good mix of configuration system improvements and some accessibility testing that'll help me understand where I stand before pushing forward on compliance work.

## The Main Work

**Generate accessibility report for location views** - I need to get a clear picture of where my accessibility violations actually are in the location views. With only 30% accessibility compliance overall, I'm flying blind right now. This report will give me concrete data to work with and help me prioritize the most impactful fixes. Plus, it's a relatively contained task that'll give me momentum.

**Add getBoolean/getTenantAware helpers** - These helper methods for the configuration system have been on my mind for a while. I keep writing verbose code to check boolean settings and handle tenant-aware configurations. Adding these helpers will clean up a lot of repetitive code across the platform and make the configuration system more ergonomic to work with.

**Create SystemSettingPolicy for RBAC** - I need proper authorization around system settings before I can confidently roll out the configuration management features. This policy will ensure that only authorized users can view and modify settings, which is crucial given that some of these settings affect security and compliance. It's a bit more involved than the helpers, but it's blocking other configuration work.

**Extend SystemSettingsSeeder with all defaults** - Once I've got the helpers and policy in place, I want to make sure my seeder is comprehensive. I've been adding settings piecemeal, and I need to do a proper audit and ensure all the defaults are documented and seeded correctly. This will prevent configuration drift between environments and make onboarding new developers smoother.

## Housekeeping

**Fix FluentCrmAdapter.php PHPStan errors** - This file is at the top of my PHPStan offenders list with 37 errors. I've been avoiding it, but it's part of a critical integration and those errors are probably masking real issues. I should at least spend some time understanding what's wrong and maybe knock out the easy fixes.

**Address the test-refactor planning directory** - I've got research done that shows ADR-0001 and my testing documentation require container-scoped Tests/ directories, but I haven't created an implementation plan yet. I should at least spend 30 minutes sketching out what this refactor would look like so it's ready when I have bandwidth for the actual work.

## Parked

I'm deliberately not touching the Groundhogg idempotency work today - that's a 3-effort task that needs focused time, and I want to knock out these foundational pieces first. The feature flag work for the unified build health dashboard is also sitting there, but the configuration system improvements feel more urgent since they're blocking multiple feature sets. I'll circle back to these tomorrow or later in the week.