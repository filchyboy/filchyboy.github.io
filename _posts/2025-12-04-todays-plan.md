# Daily Plan - Thursday, December 04, 2025

## Today's Theme
I'm pushing to complete the build-in-public automation that's been sitting in my planning directory for too long. I want to get this working end-to-end so I can start publishing my daily progress automatically instead of manually crafting blog posts every time.

## The Main Work

**Create the publish_to_jekyll.py foundation** - I need to build the core CLI structure and get the basic file operations working. This is where the rubber meets the road for automating my blog posts from the accomplished work units.

**Wire up the data loading functions** - I'll implement both modes: loading from work_units.json with date filtering and loading from accomplished.json. The accomplished.json path is what I'll use most often, but having both options gives me flexibility.

**Build the grouping and markdown generation** - This is the heart of the automation - taking my completed work units and organizing them by feature set, then generating readable Jekyll markdown. I want the output to match the style I've been using manually.

**Test the dry-run workflow** - Before I risk breaking anything, I need to implement the --dry-run flag and verify the generated markdown looks correct. I'll use this to preview posts before they go live.

**Add the Makefile targets** - I want simple commands like `make build-in-public-publish` and `make build-in-public-preview` so this becomes part of my daily routine without friction.

## Housekeeping

**Import the existing schemas** - I have validation schemas sitting in utils/schemas.py that I should pull into this new script. No point reinventing the wheel when I already have the data structures defined.

**Check on that failing PHP test** - My test suite shows 1 failed test out of 2804. That's a 96.1% pass rate which isn't terrible, but I should at least identify what's broken before it becomes a bigger problem.

## Parked

The DSR security work is sitting there with higher effort tasks, but I want to get this build-in-public automation working first. Those Phase 7 acceptance criteria can wait another day - this automation will save me time every single day going forward.