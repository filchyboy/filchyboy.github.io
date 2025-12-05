---
layout: post
title: "Daily Plan - 2025-12-05"
date: 2025-12-05
---

# Daily Plan - Friday, December 05, 2025

## Today's Theme

I'm wrapping up the week by polishing the build-in-public tooling. I've got a solid set of small, focused tasks that will make my daily publishing workflow much smoother. It feels good to spend a Friday building developer experience improvements that I'll benefit from immediately.

## The Main Work

**Build out the core publish_to_jekyll.py script structure.** I need to create the base file with proper CLI argument parsing. This is the foundation for everything else - getting the flags right (`--dry-run`, `--from-accomplished`) and setting up a clean command structure will make the subsequent work much easier for me. I'll use Click or argparse to keep it simple.

**Implement the data loading functions.** I need two separate paths: one that loads `accomplished.json` directly when I use the `--from-accomplished` flag, and another that loads `work_units.json` and filters by `completed_at` date for the default behavior. These are distinct use cases and I want both available depending on how I'm working that day.

**Add the grouping logic.** Once I can load completed work units, I need to group them by `feature_set` so my blog posts have a nice structure. This is where the schemas from `utils/schemas.py` come in - I should import those validation utilities to make sure I'm working with clean data.

**Wire up the Makefile target.** I want a simple `make build-in-public-publish` command that I can run without thinking. This ties everything together and makes the tool actually usable in my daily workflow.

## Housekeeping

**Import those existing schemas from utils/schemas.py.** I know there's validation logic already written - I should reuse it rather than reinventing the wheel. This will also help me maintain consistency across my tooling.

**Implement the --dry-run flag properly.** I'll inevitably want to preview what's going to be published before it actually writes files or pushes to Git. Building this in from the start will save me headaches when I accidentally publish something incomplete.

## Parked

Nothing's explicitly blocked right now, which is nice. The quality reports show plenty that needs attention - PHPStan errors, failing tests, Porto compliance issues - but those aren't urgent for today. I'm choosing to invest in my own productivity tooling instead, and I'm comfortable with that trade-off on a Friday.