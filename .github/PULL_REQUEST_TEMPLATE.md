<!--
  Thanks for contributing! Please fill out the sections below. Brevity is fine -
  the goal is to give the reviewer the context they need to evaluate the change.
-->

## Summary

<!-- 1-3 sentences. What does this PR do and why? -->

## Type of Change

<!-- Check all that apply -->

- [ ] `feat` - new pack content (mods, config tuning)
- [ ] `fix` - bug fix (wrong `side` tag, broken config, mis-pinned file)
- [ ] `refactor` - restructuring with no player-visible change
- [ ] `docs` - documentation only
- [ ] `chore` - tooling, build, or infrastructure
- [ ] `ci` - CI/CD changes
- [ ] `perf` - load-time or runtime performance

## Scope Check

<!-- Ribbit Survival ships a packwiz manifest + config overrides only. Confirm this
     change doesn't require Java. -->

- [ ] This change is pack-side only (mod set, config overrides, pack metadata, docs)
- [ ] If a Java change is implied, a corresponding issue exists on [productive-frogs](https://github.com/Flatts3000/productive-frogs/issues) - link it below

## Mods Touched (if any)

<!-- List added/removed/updated mods. Confirm sourcing + side tags. -->

- [ ] New mods are CurseForge-sourced (`packwiz cf add`) so the export stays a clean CF manifest
- [ ] Any Modrinth-only mod added is redistribution-licensed (LGPL/MIT) and I noted why CF wasn't used
- [ ] Verified no mod I touched dropped from the export due to a `side` tag

## Testing

<!-- How did you verify the change in-game? An export that builds isn't enough. -->

- [ ] `packwiz refresh` runs clean at the repo root
- [ ] `packwiz curseforge export` succeeds (exit 0) and `manifest.json` lists the mods I touched
- [ ] Loaded the pack in a fresh world and verified the change
- [ ] N/A - docs-only

## Docs Impact

- [ ] No docs changes needed
- [ ] Docs updated in this PR (list files below)
- [ ] `CHANGELOG.md` updated under the relevant section

## Notes for Reviewer

<!-- Anything reviewers should pay extra attention to? Known limitations?
     Screenshots welcome. -->
