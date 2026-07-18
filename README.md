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

**v0.1 built** (branch `feat/v0.1-mod-list`). **78 mods** pinned (73 CurseForge + 5 Modrinth-sourced
LGPL mods bundled on export), Productive Frogs pinned to the `26.1.2` alpha, and a trimmed PF config
override with the **Equivalence (EE) lane enabled**. `packwiz curseforge export` builds clean. Not yet
smoke-tested in a live NeoForge instance and not merged to `main`. See
[`docs/handover.md`](docs/handover.md) section 12 for the full build result, what was deferred, and
the remaining steps.

## Layout

```
pack.toml        packwiz pack metadata (name, versions, index pointer)
index.toml       file index (populated as mods are added)
mods/            per-mod .pw.toml metafiles (added via `packwiz cf add`)
config/          config overrides shipped with the pack (e.g. Productive Frogs tuning)
docs/            pack design + handover
```

## Working on the pack

```bash
packwiz cf add <slug>        # add a CurseForge mod, pins the exact 26.1.2 file
packwiz update --all         # bump pinned files to newest 26.1.2 builds
packwiz refresh              # rebuild index.toml after manual edits
packwiz curseforge export    # produce the CurseForge .zip for upload
```

Target distribution: **CurseForge**. Source every mod from CurseForge (`packwiz cf add`) so the export
is a clean CF manifest with no bundled overrides.
