# Contributing to Ribbit Survival

Thanks for your interest in contributing! Ribbit Survival is a **normal-survival content modpack** built around [Productive Frogs](https://github.com/Flatts3000/productive-frogs) - frogs that farm resources, hunt mobs for their drops, and arm boss altars, backed by an AE2 + Powah tech spine. This document covers how to file issues, what belongs here vs. upstream, and how to submit pull requests.

## No bounties, no automated PRs

This project does **not** offer bounties and does not participate in Opire, Algora, or any other third-party bounty platform. There is no payment for any issue or pull request. Comments invoking bounty-platform commands (`/opire`, `/algora`, `/try`, and the like) are ignored, and an issue showing up on a bounty board does not mean one is offered here.

**Unsolicited automated / bot pull requests are closed without review.** Machine-generated "automated fix by [bot]" PRs consistently target the wrong loader or Minecraft version, fail to compile, and exist to farm bounty platforms or contribution history. If you are a human who genuinely wants to work on an issue, say so in a comment first, then open the PR yourself.

## Scope: what belongs in this repo

Ribbit Survival is a [packwiz](https://packwiz.infra.link/) pack definition: one `.pw.toml` metafile per mod, plus config overrides. **It ships no mod jars, and no Java code lives here.** If a contribution would require new mod behavior - new blocks, items, entities, hooks, or registry-level changes - file it against [Productive Frogs](https://github.com/Flatts3000/productive-frogs/issues) instead and reference the pack-side need.

Acceptable contributions to this repo:

- Pack metadata (`pack.toml`, `index.toml`, mod `.pw.toml` metafiles under `mods/`)
- Mod config overrides (`config/`) that ship with the pack
- Pack-level docs (`docs/`, `README.md`)

If you're not sure where something belongs, open a Discussion before writing anything.

## Reporting Issues

- **Pack bugs**: open an issue using the **Bug Report** template. Include the pack version, Minecraft version, NeoForge version, launcher (CurseForge / Prism / other), and steps to reproduce. Attach `latest.log` from `.minecraft/logs/` - long logs go in a gist.
- **Mod inclusion suggestions**: use the **Mod Suggestion** template. The pack is intentionally curated toward a Productive-Frogs-centered survival loop with a lean tech spine, not a kitchen sink. Suggestions that fill a clear gap in that loop are the ones most likely to land.
- **Design / progression feedback**: use the **Feature Request** template. Frame it as the problem you're trying to solve, not just the change you want.
- **General questions**: use [GitHub Discussions](https://github.com/Flatts3000/ribbit-survival/discussions) rather than the issue tracker.

Don't open issues for security vulnerabilities - see [SECURITY.md](./SECURITY.md).

### Issues that belong upstream, not here

| Symptom                                            | Where to file                                                             |
|----------------------------------------------------|----------------------------------------------------------------------------|
| A specific frog behaves wrong                       | [productive-frogs](https://github.com/Flatts3000/productive-frogs/issues)  |
| A specific mod crashes or misbehaves on its own     | That mod's issue tracker                                                   |
| The pack's config tuning feels off (drop rates, EE) | Here - Feature Request or Bug Report, whichever fits                        |
| The pack won't launch / a mod is missing on export  | Here - Bug Report                                                          |
| You want a new modded resource to be frog-farmable  | [productive-frogs](https://github.com/Flatts3000/productive-frogs/issues) (variants are a mod feature) |

## Submitting Pull Requests

### Branching

- `main` is protected - all changes land via PR.
- Create a feature branch from `main` named like `feat/add-flux-networks` or `fix/powah-ee-config`.
- Don't push directly to `main` (docs-only changes by the maintainer are the exception).

### Commit Messages

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>: <short subject>

<body - explain WHY, not what>
```

Types we use:

- `feat:` - new pack content (mods, config tuning)
- `fix:` - bug fix (wrong `side` tag, broken config, mis-pinned file)
- `refactor:` - restructuring with no player-visible change
- `docs:` - documentation only
- `chore:` - tooling, build config, infrastructure
- `ci:` - CI/CD changes
- `perf:` - load-time or runtime performance work

One logical change per commit. Squash trivially-related work locally before PR.

### Content Quality Expectations

- **Stay in scope.** Ribbit Survival is Productive Frogs + a lean tech spine (AE2, Powah) + a curated content/QoL layer, in a **normal survival world** (not skyblock). The bar for adding a mod outside that thesis is high and needs a written rationale.
- **Source mods from CurseForge.** Use `packwiz cf add <slug>` so the export stays a clean CF manifest with no bundled overrides. A Modrinth-only mod can only ship if its license permits redistribution in a modpack (LGPL/MIT); prefer the CF source when one exists.
- **Mind the `side` tag.** packwiz sometimes sets `side = "server"` or `"client"` from the source metadata. Worldgen/structure and content mods must be `side = "both"` or they drop from the client export. Verify after adding.
- **Don't add mods casually.** Each new mod is a maintenance and load-time tax. PRs that add mods need a one-paragraph justification against the pack thesis above.
- **Docs in the same PR.** Pack changes that affect the player experience should update the relevant `docs/*.md` and add a `CHANGELOG.md` entry.

### Before You Open a PR

1. `packwiz refresh` runs cleanly at the repo root.
2. `packwiz curseforge export` succeeds (exit 0) and the resulting `manifest.json` lists the mods you touched.
3. No mod you added silently dropped from the export because of a `side` tag.
4. Docs + `CHANGELOG.md` updated where relevant.
5. PR description explains the **why** - the **what** is in the diff.

### Review

- The maintainer reviews when bandwidth permits - this is an OSS hobby project, expect days, not hours.
- Review feedback is collaborative; address comments or push back if you disagree. Both are fine.
- Approved + green CI + no unresolved threads -> maintainer squash-merges. `main` enforces squash-only and deletes the branch on merge.

## What We Probably Won't Accept

- **Fabric / Quilt support.** Ribbit Survival is NeoForge-only by design - Productive Frogs is NeoForge-only.
- **Skyblock conversion.** This is a normal survival pack on purpose. Productive Frogs' Spawnery (skyblock bootstrap) stays OFF.
- **Kitchen-sink mod additions.** "I like this mod" isn't a justification; "this supplies a resource tier or logistics layer the pack is missing" is.
- **Java mods bundled into the pack.** If a feature needs Java, it goes in [productive-frogs](https://github.com/Flatts3000/productive-frogs).
- **Balance changes without playtesting evidence.** A drop-rate or config tweak needs to come with "I played through it and here's what I observed."

## Maintainer Cadence

This is a hobby OSS project. Realistic expectations:

- Issue triage: within ~1 week of opening.
- PR review: ~1 week, sometimes longer.
- Releases: irregular, driven by significant content batches, upstream Productive Frogs releases, or critical fixes.

If something is urgent (security, major upstream break), ping the maintainer in the relevant issue/PR; they'll prioritize.

Thanks again for contributing! 🐸
