# Ribbit Survival

A normal-survival Minecraft modpack for **NeoForge 26.1.2.76 / Minecraft 26.1.2**, built around
[Productive Frogs](https://www.curseforge.com/minecraft/mc-mods/productive-frogs) (CurseForge project
`1552728`) as its centerpiece content mod. Not a skyblock - a regular world with frogs that farm
resources, hunt mobs for their loot, and arm boss altars.

This repo is the **pack definition only** (a [packwiz](https://packwiz.infra.link/) manifest: one
`.pw.toml` metafile per mod, plus config overrides). It ships no mod jars. The mod source for
Productive Frogs lives in the sibling repo `../productive-frogs` and is pinned here like any other
dependency.

## Status

**v0.1.0 shipped to CurseForge (alpha), pending first-file moderation.** Uploaded 2026-07-18 (file
`8458262` on CurseForge project `1615242`). **78 mods**, **all CurseForge-sourced** so the export is a
clean CF manifest with no bundled jars. Productive Frogs is pinned to its `26.1.2` alpha, and a trimmed
PF config override ships the **Equivalence (EE) lane enabled**. In-world load confirmed before release.

Releases from v0.2.0 onward are automated: push a `vX.Y.Z` tag and CI builds the export, cuts a GitHub
release, and uploads to CurseForge. See [`docs/handover.md`](docs/handover.md) section 12 for the full
build record and distribution details.

## Links

- **CurseForge:** https://www.curseforge.com/minecraft/modpacks/ribbit-survival (live once moderation clears)
- **Productive Frogs** (the centerpiece mod): https://github.com/Flatts3000/productive-frogs
- Issues and Discussions: this repo's [Issues](https://github.com/Flatts3000/ribbit-survival/issues) and [Discussions](https://github.com/Flatts3000/ribbit-survival/discussions) tabs.

## Layout

```
pack.toml        packwiz pack metadata (name, versions, index pointer)
index.toml       file index of everything the pack ships
mods/            per-mod .pw.toml metafiles (added via `packwiz cf add`)
config/          config overrides shipped with the pack (e.g. Productive Frogs tuning)
branding/        logo + CurseForge icon (uploaded to CF, not bundled in the pack zip)
docs/            pack design + handover
.github/         issue/PR templates, dependabot, tag-driven release workflow
```

`.packwizignore` keeps `docs/`, `branding/`, and build artifacts out of the distributed
pack zip; the CurseForge project icon is set from `branding/` via the CF dashboard.

## Working on the pack

```bash
packwiz cf add <slug>        # add a CurseForge mod, pins the exact 26.1.2 file
packwiz update --all         # bump pinned files to newest 26.1.2 builds
packwiz refresh              # rebuild index.toml after manual edits
packwiz curseforge export    # produce the CurseForge .zip for upload
```

Target distribution: **CurseForge**. Source every mod from CurseForge (`packwiz cf add`) so the export
is a clean CF manifest with no bundled overrides.
