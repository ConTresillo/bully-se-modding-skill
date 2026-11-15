# Native scripts, asset mods and platform boundaries

This reference combines community documentation from the pinned `RanggaBS/bully-scripting` snapshot and SimonBestia's [Bully Modding Documentation](https://github.com/SimonBestia/Bully-Modding-Documentation) (audited commit `e14c2a85d5608aa205dca56a065044d8a90b7d19`). Simon's site calls itself incomplete and invites people to reuse information with credit; this skill summarizes it and links to pages rather than redistributing the site. Confirm the exact page/version before acting.

## Choose the right mod path
- **New gameplay behavior:** prefer a DSL script collection; it avoids replacing `Scripts.img` files and supports collection start/stop/restart.
- **Replace a native script:** use only when the task needs the native script's startup/mission position or DSL cannot provide the required behavior. The community Lua resource says Bully uses Lua 5.0.2 with 4-byte floating-point numbers; compile with a compatible compiler and test a round-trip before replacing any archive entry.
- **Asset replacement:** identify exact PC format/archive and use a reversible overlay or backup. Never edit the live archive while the game is running; Simon's stream guide warns PC archive editing during runtime may permanently corrupt it.
- **Online behavior:** only if explicitly requested; establish whether DSL/DSS Sync APIs cover it, validate on an isolated server, and get authorization before exposing ports or deploying a server.

## File/format map (PC-focused; verify platform before reuse)
- `Scripts.img` / `.dir`: native script archive; `.lur` is compiled Lua script. DSL can load source Lua in collections, but native replacements still use the game's compatible script format.
- `World.img`: world-related assets such as peds, weapons, map props; PC model references use `.nif`, associated textures commonly `.nft`.
- `.act`: source action-tree format; `.cat`: compiled/compressed action tree. These are not interchangeable with platform variants; community docs warn action data can differ by version/platform.
- `IDE.img` / `default.idb`, `DAT`/trigger files, stream and texture assets: use exact current PC references and a file-format-specific tool; old forum guidance may be stale.
- PS2/Wii/Xbox 360 lists, debug-build files, or binary endianness are not valid substitutes for PC data. Keep each platform's IDs/assets separate.

Sources: [stream basics](https://github.com/SimonBestia/Bully-Modding-Documentation/blob/e14c2a85d5608aa205dca56a065044d8a90b7d19/Modding/Resources/STREAMRelated/General.html), [models](https://github.com/SimonBestia/Bully-Modding-Documentation/blob/e14c2a85d5608aa205dca56a065044d8a90b7d19/Modding/Resources/STREAMRelated/Models.html), [action trees](https://github.com/SimonBestia/Bully-Modding-Documentation/blob/e14c2a85d5608aa205dca56a065044d8a90b7d19/Modding/Resources/ACTRelated/ActionNodesList.html), [mission/minigame IDs](https://github.com/SimonBestia/Bully-Modding-Documentation/blob/e14c2a85d5608aa205dca56a065044d8a90b7d19/Modding/Resources/SCRIPTSRelated/IDs/MissionMinigame.html).

## Model authoring — high-risk, follow the exact current page
SimonBestia's model page gives a PC `.nif` workflow for its tested Blender Niftools setup: reset/apply object transforms; use UV map `UV0`; use face-corner byte-color attribute `RGBA` (BCBCBC); use a game-compatible BULLY material; during export turn off “Force DDS” and “Optimise Materials”; in NifSkope set each relevant `NiTexturingProperty` Base Texture `Flags` to `12800`. Its notes warn Jimmy clothes refuse more than one texture, multiple materials on one mesh are unsupported, and some models need `NiStencilProperty` flags `19840` for backface culling. Tool versions and game support may have changed; verify the current page, test one expendable asset and keep original `.nif`/`.nft` backups. A bad flag/material can crash the game; never bulk-replace before a successful single-model test.

## Action-tree editing — reverse-engineered, experimental
The community action-tree guide explains that nodes contain conditions and tracks, and that an action combines animation with other effects (sound/effects). It recommends comparing source `.act` to compiled/decompiled `.mact`: many condition/track parameters remain generically named and values can have different representations. Its `mact` tool is for decompressing `.cat` to `.mact` and recompressing changes. Treat PC, PS2, Xbox 360, Wii and debug-build lists separately; the guide warns data may not be cross-compatible. Do not ship or run debug-build game assets. Keep an unchanged backup and test a tiny change in a disposable copy/save.

## Reference data lookup
SimonBestia's site includes PC-oriented mission/minigame IDs, flags, areas, quotes, sound effects, weather, clothing/hair and action-node lists. The pages explicitly mark some data incomplete or edition-specific. Resolve each identifier in the page for the target PC edition; do not take a PS2/Wii/debug index by default. `RanggaBS/bully-scripting` separately contains enumerations and object/model data; its mission-index page labels dummy missions “DO NOT RUN.” These are clues, not runtime guarantees.

## Before touching archives
1. Confirm Steam/retail build, game version and exact archive/file extension.
2. Close the game; copy the whole affected archive and its paired `.dir` (if present) and record hashes.
3. Use a maintained tool with explicit Bully PC format support; never patch an IMG/dir with a generic GTA assumption.
4. Make one minimal edit in a duplicate/test installation; rebuild, verify archive listing and file sizes, launch, test behavior, and confirm a clean uninstall path.
5. If a tool or format lacks reliable PC support, stop and report the gap instead of using random binaries, leaked debug builds, or speculative hex edits.
6. Do not redistribute game data, decompiled original scripts, debug builds, or assets unless the user has rights and the license permits it.
