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
3. Add the rest of section 5 with `packwiz cf add <name>`, accepting dependency prompts. Batch it;
   note any mod/dep that has no 26.1.2 file and defer it.
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
