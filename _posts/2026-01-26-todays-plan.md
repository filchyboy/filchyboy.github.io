---
layout: post
title: "Daily Plan - 2026-01-26"
date: 2026-01-26
---

# Daily Plan - Monday, January 26, 2026

## Today's Theme
I'm picking up right where I left off yesterday with the SCSS hard-code refactor work - I was deep in this yesterday so all the context is still fresh in my head. This feels like the natural continuation, and I've got good momentum on cleaning up our CSS variable patterns. I'll also squeeze in some internationalization work since I've been actively developing that feature set over the past week.

## The Main Work

**scss-p1-plugin-exclude-tokens: Update plugin to exclude _tokens.scss pattern**
I worked on this yesterday so the PostCSS plugin logic is still loaded in my brain. This is the foundation for the other SCSS refactor tasks, so getting this right will make everything else flow smoothly.

**scss-p1-config-excludes: Update postcss.config.cjs excludeFiles**
Since I'll have just updated the plugin logic, configuring the exclude patterns is the natural next step. The context will be fresh and I'll be able to validate that the plugin changes work correctly.

**scss-p1-plugin-css-fallback: Add CSS variable fallback pattern to excludePatterns**
This builds directly on the previous two tasks - I'll be in the same files and the same headspace around CSS variable handling and exclusion patterns.

**i18n-p7-unit-locale-resolution-2: Test locale resolution: Accept-Language header**
I've been actively working on internationalization this week with 6 commits, so the locale resolution logic is familiar territory. This feels like a good change of pace from the SCSS work while staying in feature sets where I have momentum.

**scss-p1-plugin-project-file-helper: Add isProjectFile() helper function for strict mode**
I'll circle back to the SCSS work to add this helper function. By this point in the day, I'll have a solid understanding of how the exclusion patterns are working and can build the project file detection logic.

## Housekeeping

**Run `make lint-fix` to auto-fix ESLint issues**
This will clean up 1,230 auto-fixable warnings in one command - satisfying progress with minimal effort.

**Refresh lint harness snapshot**
The reports are 17 days stale, so running `make lint-harness-snapshot` will give me current visibility into code quality.

**Draft implementation plan for tailwind-migration**
Since I'm already thinking about CSS patterns with the SCSS refactor work, this is good timing to plan the Tailwind migration. The research is done and it's 39% complete, so having a concrete implementation plan would help me tackle this systematically.

## Parked

I'm setting aside the remaining SCSS strict mode tasks (scss-p1-config-strictmode and scss-p1-plugin-strict-report) for tomorrow. I want to get the core exclusion logic solid first before adding the strict mode complexity. The second internationalization test can also wait - better to make real progress on fewer items than to spread myself thin.