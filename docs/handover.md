# Ribbit Survival - Handover

**Written:** 2026-07-17. **For:** the next Claude session (or human) picking up this pack.
**Repo:** `F:\minecraft-repos\ribbit-survival` (sibling to the mod repo `F:\minecraft-repos\productive-frogs`).

This is the single authoritative context doc. Read it top to bottom before touching the pack. It
records what was decided, why, the availability data behind the mod list, and the exact next steps.

---

## 1. What this is

A **normal-survival** (NOT skyblock) NeoForge modpack for **MC 26.1.2 / NeoForge 26.1.2.76**, built
around **Productive Frogs** as the marquee content mod. Distributed on **CurseForge**.

The pack is a separate project from the mod on purpose: different artifact, different CurseForge
project, different release cadence. Productive Frogs (CurseForge project `1552728`) is pinned here as
a dependency like any other mod. Do not couple the two repos.

## 2. Decisions already made (do not relitigate)

| Decision | Value | Notes |
|---|---|---|
| Pack name | **Ribbit Survival** | repo dir, `pack.toml` name, future CF project title |
| Distribution | **CurseForge** | source every mod from CF so the export is a clean CF manifest |
| World type | **Normal survival** | PF 2.0 is a normal-world content mod; the Spawnery (skyblock bootstrap) stays OFF |
| Scope | **Mid-size** with a tech spine | PF is the star; a lean AE2 + Powah spine, not a kitchen sink |
| MC / loader | **26.1.2 / NeoForge 26.1.2.76** | matches PF's current target exactly - no PF version bump needed |
| Repo location | `F:\minecraft-repos\ribbit-survival` | git initialised, branch `main` |
| Pack tool | **packwiz** | installed on this machine; same tool Sky Frogs pins |

## 3. The strategic thesis (why launch now)

26.x modpacks are sparse **because the marquee content and tech mods are not ported yet** - Create,
Mekanism, Thermal, Immersive Engineering, Industrial Foregoing, Farmer's Delight, and Supplementaries
all have **no 26.x build** as of 2026-07-17. The utility layer (performance, QoL, worldgen) is fully
current on 26.1.2, but content is the scarce ingredient.

That is the opening: **a content mod is the scarcest thing in the 26.1 ecosystem, and we own one.**
The strong position is PF as the marquee content mod of an early 26.1 survival pack, not PF buried in
a kitchen-sink pack (which can't be built anyway right now). Sparse field + we supply the scarce
ingredient = real differentiation, near-zero competition, early-adopter discoverability on CurseForge.

Growth path is additive: when Create / Mekanism / Farmer's Delight land on 26.x, each drops into a
pack update and is a "new content added" release that re-surfaces the pack.

## 4. Availability data (Modrinth API, NeoForge, checked 2026-07-17)

`26.1.2 YES` = has a NeoForge build on MC 26.1.2 (PF's target). Method: Modrinth
`/v2/project/<slug>/version?loaders=["neoforge"]`, filtered to game versions starting `26`. The
sibling repo's `scripts/fetch_dev_mods.py` is the reusable pattern (but it is pinned to 1.21.1 - do
not trust it for 26.x).

**Available on 26.1.2 (viable pack ingredients):**
- Performance: `sodium`, `lithium`, `ferrite-core`, `modernfix`, `entityculling`
- QoL: `jei`, `jade`, `curios`, `sophisticated-backpacks`, `sophisticated-storage`, `xaeros-minimap`, `xaeros-world-map`
- Worldgen: `terralith`, `tectonic`, `yungs-better-mineshafts`, `explorers-compass`
- Tech spine: `ae2` (Applied Energistics 2), `powah`
- Flavor: `structory`, `macaws-furniture`, `macaws-doors`

**NOT on 26.x yet (confirmed absent - do not plan around these; add later as they port):**
Create, Mekanism, Thermal Expansion, Immersive Engineering, Industrial Foregoing, Farmer's Delight,
Supplementaries, Chipped, Handcrafted, EMI (JEI covers this), Croptopia, When Dungeons Arise,
Cataclysm, Aquamirae.

Note: many of the available mods are ALSO on 26.2, and 26.3 is in snapshots - the ecosystem is past
26.1.2. We stay on 26.1.2 because that is PF's target and every mod above has a 26.1.2 build. See
watch-item in section 9.

## 5. Locked v0.1 mod list

Source everything from **CurseForge** (`packwiz cf add <slug-or-search>`). Slugs below are the
Modrinth slugs used for the availability check; the CF project is the same mod - search by name if the
CF slug differs. `packwiz cf add` prompts to resolve required dependencies; accept them.

| # | Mod | Role | Dep notes |
|---|---|---|---|
| 1 | **Productive Frogs** | THE content star | CF project `1552728`, releaseType alpha, current `2.0.0-alpha.2`. See section 6. |
| 2 | Sodium | rendering perf | - |
| 3 | Lithium | tick/game perf | - |
| 4 | FerriteCore | memory | - |
| 5 | ModernFix | perf / patches | - |
| 6 | EntityCulling | render perf | - |
| 7 | JEI | recipe viewer | PF ships JEI integration (subtype interpreters, recipe categories) |
| 8 | Jade | in-world tooltips | PF ships a Jade plugin |
| 9 | Curios API | accessory slots | PF's Brewed Froglight charm slot targets Curios (currently on hold in PF, harmless to include) |
| 10 | Sophisticated Backpacks | portable storage | pulls Sophisticated Core |
| 11 | Sophisticated Storage | block storage | pulls Sophisticated Core |
| 12 | Xaero's Minimap | navigation | - |
| 13 | Xaero's World Map | navigation | - |
| 14 | Terralith | overworld worldgen | Stardust Labs; coexists with Tectonic |
| 15 | Tectonic | terrain shape | Stardust Labs; coexists with Terralith |
| 16 | YUNG's Better Mineshafts | structure | may pull YUNG's API |
| 17 | Explorer's Compass | find structures | may pull a YUNG/util lib |
| 18 | Applied Energistics 2 | storage/automation spine | - |
| 19 | Powah | RF power spine | pulls Cloth Config + GuideME (per PF's dev-mod notes) |
| 20 | Structory | structures | - |
| 21 | Macaw's Furniture | decoration | - |
| 22 | Macaw's Doors | decoration | - |

~22 mods incl. PF - genuine mid-size for an early-26.1 pack. If a dep (e.g. Sophisticated Core,
GuideME, Cloth Config, YUNG's API) is not on 26.1.2 when you go to add it, that mod drops from v0.1;
note it and move on rather than blocking the whole pack.

## 5b. QoL mods harvested from Sky Frogs (user request, 2026-07-17)

The user wants "as many QoL mods that are in Sky Frogs that have updated to 26.x." Sky Frogs is the
sibling pack at `F:\minecraft-repos\sky-frogs\pack\` (155 mods, MC 1.21.1). Its QoL subset was checked
against the Modrinth NeoForge API for 26.x. Add all of tier A; verify tier B at add-time (they are
CurseForge-primary, so `packwiz cf add` is the real test); skip tier C.

**Tier A - confirmed 26.1.2, ADD these (21):**
`appleskin`, `clumps`, `controlling`, `crafting-tweaks`, `inventory-essentials`, `mouse-tweaks`,
`trashslot`, `searchables`, `toast-control`, `fastfurnace`, `fastsuite`, `fastworkbench`,
`simple-magnets`, `item-collectors`, `gravestone-mod`, `construction-sticks`, `cooking-for-blockheads`,
`iron-furnaces`, `trash-cans`, `simple-backups`, `framedblocks`, `connected-glass`.

**Tier B - not on Modrinth, verify on CurseForge via `packwiz cf add` (add if a 26.1.2 file exists):**
`jade-addons`, `extreme-sound-muffler`, `just-enough-professions` (JEP), `just-enough-resources` (JER),
`ftb-ultimine`, `ftb-chunks`, `spice-of-life-carrot-edition`, `mob-grinding-utils`, `building-gadgets`.
(JEP/JER/jade-addons are high value - they extend the JEI/Jade experience PF already integrates with.)

**Tier C - NO 26.x build yet, DEFER (re-check on later pack updates):**
`polymorph`, `configured`, `more-overlays-updated`, `fast-leaf-decay`, `inventory-tweaks-refoxed`,
`torchmaster`, `not-enough-wands`. (Content mods `chipped` and `supplementaries` are also still absent,
per section 4.)

Notes: `searchables` and `sophisticated-core` and similar are libraries some of the above need - accept
`packwiz cf add` dependency prompts. Skyblock-only Sky Frogs mods (`skyblock-builder`, `ex-deorum`,
`cobblegen-galore`, `forgiving-void`, `sky-guis`, the FTB quests/teams/ranks stack) are intentionally
NOT carried over - Ribbit Survival is a normal world.

## 6. Pinning Productive Frogs (the important one)

- CurseForge project **`1552728`**. It ships as **releaseType `alpha`**, game version `26.1.2`, Java 25.
- Current version at handover: **`2.0.0-alpha.2`** ("Closing the Hatch"). Confirm the newest 26.1.2
  alpha at add-time.
- `packwiz cf add` may hide alpha files by default - if PF does not appear, add by explicit
  project/file id, or verify the file's release channel. Do NOT substitute a 1.21.1 file (the mod has
  two lines; the 1.21.1 line is frozen at `1.24.x`). The 26.1 jar name carries the MC version:
  `productivefrogs-26.1.2-2.0.0-alpha.2.jar`.
- The mod source + full design lives in `../productive-frogs`. Its `CLAUDE.md` and
  `docs/modpack_integration.md` are the authoritative reference for every PF config knob and tag.

## 7. Integration hooks to lean into (the pack's identity)

These work TODAY with the available mods, no PF cross-mod code needed (PF's own cross-mod JSON layer
is on hold for 26.1 - see `../productive-frogs/CLAUDE.md`, "Integrations"):

- **Powah RF -> PF's Equivalence (EE) lane.** PF's Alembic and Distiller are RF-powered via the
  standard `Capabilities.Energy.BLOCK` capability (`ReceiveOnlyEnergyHandler`). Powah's generators and
  energy cells feed them directly. This is a real, working integration and a natural pack hook: power
  your frog transmutation lane with Powah. NOTE: the EE lane is **default OFF** in PF
  (`equivalenceEnabled`, fail-closed) - if the pack wants to feature it, enable it in the PF config
  override (section 8) and verify in-world.
- **AE2 storage** for the loot the predator/Apex frogs and boss altars produce (raw boss drops, XP as
  Liquid Experience buckets). AE2 fluid storage can hold PF's fluids (Slime Milk, Mob Slurry, Liquid
  Experience) since they use the standard `Capabilities.Fluid` handlers.
- **JEI + Jade** already have first-party PF integration - they make PF's mechanics legible, which
  matters for a pack whose whole point is showcasing PF. Keep both.

## 8. Config overrides to plan (`config/`)

The pack should ship a tuned PF config as an override so players get the intended experience. PF writes
`config/productivefrogs-common.toml` on first launch; ship a curated copy under this repo's `config/`
(packwiz `overrides`). Key knobs (full table in `../productive-frogs/docs/modpack_integration.md`):

- `[spawnery] enabled = false` - keep OFF (normal world has swamps). This is already the default.
- `[boss] enabled = true` and `[predators] enabled` (predation is PF 2.0's centerpiece - keep ON).
- `[equivalence]` - decide whether to feature the EE lane (default OFF). If featuring the Powah hook,
  turn it ON here. Confirm the exact key name against a generated config.
- Consider `[slime_milk] depletionEnabled` and spawn cadence for a survival (not skyblock) balance.

Do NOT hand-write the toml from memory - generate it once (launch a dev client or the pack), then trim
to only the values you intentionally override, so PF's future defaults still flow through for untouched
keys.

## 9. Watch items / gotchas

- **26.2 churn.** The ecosystem has moved past 26.1.2 (26.2 released, 26.3 snapshots). Mods will keep
  moving. We stay on 26.1.2 because that is PF's target and everything above has a 26.1.2 build. If a
  needed mod drops 26.1.2 support before we ship, the options are: pin its last 26.1.2 file, or bump
  the whole pack (and wait for PF to target 26.2). Re-run the availability check before locking.
- **`packwiz cf add` and the CurseForge API.** Verify it works without extra setup. If it needs a
  CurseForge API key, PF's repo has one in `../productive-frogs/.env` (`CURSEFORGE_API_KEY`) - do not
  copy the secret into this repo; set it in the environment for the command only.
- **PF version bump NOT needed.** MC 26.1.2 is correct; do not "upgrade" PF or the pack to chase 26.2
  without a deliberate decision.
- **Dependency availability.** Some deps (Sophisticated Core, GuideME, Cloth Config, YUNG's API) must
  themselves be on 26.1.2. `packwiz cf add` will surface this; a missing dep means that mod is deferred
  to a later pack update, not a blocker for the rest.
- **CurseForge export requires all mods CF-sourced.** If any mod ends up Modrinth-only, the CF export
  bundles it as an override only when its license permits redistribution - otherwise the export fails.
  Prefer `packwiz cf add` for everything to avoid this.

## 10. Exact next steps

1. `cd F:\minecraft-repos\ribbit-survival`
2. Add PF first and confirm the pin resolves to a **26.1.2 alpha** file (section 6):
   `packwiz cf add productive-frogs` (or by project id `1552728`).
3. Add the rest of section 5 (tech spine, worldgen, perf, flavor) AND the QoL mods in section 5b with
   `packwiz cf add <name>`, accepting dependency prompts. Add tier A of 5b outright; try tier B and keep
   whatever has a 26.1.2 CF file; skip tier C. Note any mod/dep with no 26.1.2 file and defer it.
4. `packwiz refresh`, then sanity-check `index.toml` lists everything.
5. Generate + trim the PF config override into `config/` (section 8).
6. Smoke test: point a NeoForge 26.1.2 instance (or `packwiz curseforge export` -> import into a
   launcher) at the pack; confirm it loads, PF is present, and the Powah->EE-lane + AE2 hooks behave.
7. Commit as you go (branch-local `main` in this fresh repo is fine). Do NOT create the CurseForge
   project or upload until the pack loads clean and the list is final - that is a user decision.

## 11. Reference

- Mod source + PF design: `F:\minecraft-repos\productive-frogs` (read its `CLAUDE.md` and
  `docs/modpack_integration.md`).
- packwiz docs: https://packwiz.infra.link/
- PF on CurseForge: project `1552728`.
- Availability method: Modrinth v2 API, NeoForge loader, game version `26.1.2` (rerun before locking).

## 12. v0.1 build result (EXECUTED 2026-07-17, branch `feat/v0.1-mod-list`)

The pack was built. This section records what actually landed so the next session works from the
real state, not the plan. **78 mods total** (73 in the CurseForge manifest + 5 Modrinth-sourced
externals), plus one PF config override. `packwiz curseforge export` succeeds clean (exit 0).

### Decisions locked at build time
- **EE lane is ON** (user decision). Shipped via the config override, not left at PF's opt-in default.
- **Extra content added beyond sections 5/5b** from a full-Sky-Frogs sweep (user-approved buckets):
  Tech/automation, Apotheosis RPG, and QoL/farming. The **decoration suite was offered and declined**
  (do not re-propose the 8 extra Macaw's mods / rechiseled / glassential unless the user asks).

### PF pin (confirmed)
`productivefrogs-26.1.2-2.0.0-alpha.2.jar`, CF project `1552728`, file-id `8402058`. `packwiz cf add`
resolved the alpha automatically - no explicit file-id or channel override was needed.

### Config override (`config/productivefrogs-common.toml`)
Trimmed to only the two keys we intentionally change from PF's shipping defaults; NeoForge fills the
rest from the ConfigSpec on first load. Keys set:
- `[equivalence] enabled = true` - **the featured EE lane** (PF default is FALSE/opt-in). Powered
  in-world by Powah RF -> PF Alembic/Distiller via `Capabilities.Energy.BLOCK`.
- `[spawnery] enabled = false` - normal-world identity (matches PF default; asserted for safety).

### Sourcing (matters for the CF export)
- **73 mods CF-sourced** (in the export manifest).
- **5 mods Modrinth-sourced**, all **LGPL-3.0** so the CF export bundles them into `overrides/mods/`
  cleanly: **Powah** (7.0.4-alpha), **YUNG's Better Mineshafts**, **YUNG's API**, **GuideME**,
  **Cloth Config**. These have no 26.1.x file on CurseForge yet; re-source from CF (`packwiz cf add`)
  if/when they publish one, to move them into the manifest.

### Added beyond the original plan (Sky Frogs sweep, 2026-07-17)
- **Tech/automation:** Pipez, Modular Routers, Iron Jetpacks (Powah-charged), Just Dire Things,
  Extended Crafting.
- **Apotheosis RPG:** Apotheosis, Apothic Attributes, Apothic Enchanting, Apothic Spawners (MIT; a
  deliberate content layer - high-value scarce 26.1 content).
- **QoL/farming:** OpenBlocks Elevator (resolves to the CF ElevatorID continuation), Dark Utilities,
  Crafting on a Stick, More Dragon Eggs, Squat Grow.
- **Auto-deps pulled:** Bookshelf, Cucumber, Nanite Library, Patchouli, Pig Pen Cipher, Runelic,
  Nyctography (the last three are the Darkhax family required by Dark Utilities), plus Placebo for
  Apotheosis. All required deps, all real 26.1.2 files.

### Deferred - no 26.1.x CF build AND/OR not bundle-licensed (re-check on later updates)
- From the original plan: **entityculling** (tr7zw protective license, no CF 26.1.x - client-only
  perf, already covered by sodium/lithium/ferritecore/modernfix), **crafting-tweaks** (ARR, no CF
  26.1.x), **jade-addons** (ARR on Modrinth, no CF 26.1.x - re-add from CF when it ships one, it's
  high value), **mob-grinding-utils** (only an ARR fork exists), **ftb-ultimine**, **ftb-chunks**
  (no 26.1.x build).
- From the sweep: **botany-pots**, **botany-trees**, **functional-storage**, **time-in-a-bottle**,
  **almost-unified** (on Modrinth but no 26.1.x NeoForge build), **flux-networks** (no 26.1.x CF
  build - would pair well with Powah, worth re-checking), **mamas-herbs-and-harvest** (only tags
  26.1/26.1.1, no 26.1.2 - dropped).

### Two bugs found + fixed during the build
1. **YUNG's Better Mineshafts shipped `side = "server"`** (packwiz set it from Modrinth's
   `client_side: unsupported`). That dropped it from the client-focused CF export, so singleplayer
   worlds would generate no mineshafts. Fixed to `side = "both"` in its `.pw.toml`. **Watch for this
   on any Modrinth-sourced worldgen/structure mod** - verify it survives the export.
2. **`pack.toml` had a malformed `acceptable-game-versions = ["26.1,26.1.0,26.1.1"]`** (one
   comma-joined string, matched nothing). Removed it. Every mod resolved on a real `26.1.2` tag, so
   the pack is cleanly locked to 26.1.2 with no version-widening needed. If you later need to accept a
   patch-line version, use `packwiz settings av -a 26.1` (separate entries), not a joined string.

### Still TODO (unchanged from section 10, steps 6-7)
- **In-world smoke test** (not done here - no NeoForge runtime in the build session): import the
  export zip into a launcher, confirm it loads, PF is present, and the **Powah -> EE-lane** and AE2
  hooks behave with `equivalence.enabled = true`.
- **Do NOT create/upload the CurseForge project** until the smoke test passes - that stays a user
  decision. Branch `feat/v0.1-mod-list` holds the build; not yet merged to `main`.
