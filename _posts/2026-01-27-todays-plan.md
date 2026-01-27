---
layout: post
title: "Daily Plan - 2026-01-27"
date: 2026-01-27
---

# Daily Plan - Tuesday, January 27, 2026

## Today's Theme
I'm continuing my momentum on the SCSS hard-code refactor feature set - I've got 9 commits this week and just worked on it yesterday, so all the context is fresh in my head. I also want to push forward on the internationalization work since I've been building solid momentum there too with 6 commits this week. Both of these are active feature sets where I've been investing significant time.

## The Main Work

**scss-p1-plugin-exclude-tokens: Update plugin to exclude _tokens.scss pattern**
I've been heads-down on the SCSS refactor all week and just touched this yesterday - the plugin architecture is loaded in my mind and I can make good progress here. This exclusion pattern is foundational for the other SCSS work.

**scss-p1-config-excludes: Update postcss.config.cjs excludeFiles**  
Following directly from the plugin work above, I need to wire up the configuration side. Since I'm already deep in the SCSS refactor context, this flows naturally as the next step.

**scss-p1-plugin-css-fallback: Add CSS variable fallback pattern to excludePatterns**
Another piece of the SCSS plugin puzzle that I can knock out while I'm in this domain. The fallback patterns are critical for the refactor to work correctly across the codebase.

**i18n-p7-unit-locale-resolution-2: Test locale resolution: Accept-Language header**
I've been building momentum on internationalization with 6 commits this week. The locale resolution testing is a concrete next step that I can make progress on while the i18n architecture is fresh in my mind.

**i18n-p7-unit-locale-resolution-3: Test locale resolution: user preference**
While I'm working on locale resolution tests, I should tackle the user preference testing too. These test suites are related and I can batch the work efficiently.

## Housekeeping

**Run `make lint-fix` for auto-fixable issues**
I can quickly clean up 4 errors and 1,226 warnings with a single command. Good way to start the day with some immediate progress.

**Refresh lint harness snapshot**
The reports are 18 days stale - I'll run `make lint-harness-snapshot` to get current data on the codebase health.

**Review TypeScript errors in 11 files**
26 TypeScript errors likely means missing imports or simple type issues. I can spot-check these while I'm working in the React components.

**Draft implementation plan for tailwind-migration**
This aligns with my SCSS work and the research is already done. Since I'm deep in CSS/styling context today, I can sketch out concrete next steps for the Tailwind migration while the styling architecture is fresh in my mind.

## Parked

I'm setting aside any new feature planning today to maintain focus on my active SCSS and i18n work streams. The 134 untracked commits show I've been doing significant infrastructure work lately, but I want to push forward on these tracked feature sets where I've built real momentum.