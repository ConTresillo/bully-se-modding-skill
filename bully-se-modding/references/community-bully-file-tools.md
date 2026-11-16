# Community file tools for Bully formats

## Scope and caution

The source is [EdnessP’s Tools & Plugins index](https://ednessp.github.io/tools#Bully_(Canis_Canem_Edit)) and its linked scripts in [EdnessP/scripts](https://github.com/EdnessP/scripts). The page says it is a work in progress. These are third-party format/asset utilities, not Rockstar tools or DSL gameplay scripts. Read the current source and verify the game edition, platform, tool version, and dependencies before using them. The reference page documents capabilities; it does not establish that a particular local file or release was tested here.

These utilities do *not* provide a verified way to spawn NPCs in Harrington House. Use the DSL/Lua gameplay references for runtime NPC behavior; use archive tools only when the task is specifically about the corresponding asset/file format. Back up original files and work on copies before any rebuild or in-place update.

## Tools by format and platform

- **`string_bin.py` — text containers.** The author describes import/export of `.BIN` string containers for *Bully (Canis Canem Edit)* and *Bully: Scholarship Edition* on PC, PS2, Wii, and Xbox 360. The script’s CLI uses `X` to extract to JSON and `B` to rebuild; `-be` is documented for Wii/Xbox 360 big-endian output. It contains a label-hash reimplementation; do not assume that every game build’s string set or hash map is covered. [Source](https://github.com/EdnessP/scripts/blob/main/bully/string_bin.py)

- **`hash_build.py` — Hash sound archives.** The script documents extract/build support for the Angel Studios/Rockstar San Diego Hash archive family including *Bully (Canis Canem Edit)*; the index says *Canis Canem Edit* and *Scholarship Edition* PC/PS2/Wii/Xbox 360. Its CLI distinguishes extract (`X`) and rebuild (`B`), exposes `--algo Bully`, and documents big-endian rebuilds for Wii/Xbox 360. For split Wii Speech BIN+FSB extraction it documents a separate body argument. Check the script’s Python minimum version and options before use; back up archives before rebuilds. [Source](https://github.com/EdnessP/scripts/blob/main/midnight-club/hash_build.py)

- **`BullyHash.py` — hash helpers, not an archive editor.** Reimplements Bully’s sound-name hash and string-label hash routines, with `rsm` and `str` CLI modes. The file attributes these routines to PS2 Bully functions; treat results as format/research helpers, not proof that arbitrary edition-specific data is compatible. [Source](https://github.com/EdnessP/scripts/blob/main/bully/BullyHash.py)

- **`lipfile_update.py` — speech/lip metadata repair.** Its documented job is to scan `WORLD.DIR` / paired `WORLD.IMG` and update `.LIP` metadata to match `SPEECH.BIN`. The implementation opens the IMG for in-place writing, so preserve a backup and test only on a duplicate. Its source has a narrow Wii FSB note that explicitly says full Wii support is unlikely; do not treat that as general Wii support. [Source](https://github.com/EdnessP/scripts/blob/main/bully/lipfile_update.py)

- **`BullyX360img.bms` — Wii/Xbox 360 archive extraction.** QuickBMS script for big-endian `.DIR`/`.IMG` archives. Its comments say it should work for Wii and Xbox 360, with XMem decompression handling for compressed Xbox 360 world archives. Confirm the input platform and compression state; extraction support is not a general archive-rebuild or mod-install workflow. [Source](https://github.com/EdnessP/scripts/blob/main/bully/BullyX360img.bms)

- **`fmt_BullySE_Wii.py` — Wii model/texture viewing.** Noesis plugin for Scholarship Edition Wii `.DFF` and `.TXD`; the tools index says texture display also requires the linked Nintendo texture and Wii TPL Noesis plugins. This is not a PC asset-format claim. [Plugin](https://github.com/EdnessP/scripts/blob/main/bully/fmt_BullySE_Wii.py) · [required library](https://github.com/Zheneq/Noesis-Plugins/blob/master/lib_zq_nintendo_tex.py) · [required plugin](https://github.com/Zheneq/Noesis-Plugins/blob/master/fmt_wii_tpl.py)

- **`rstm_build.py` — PS2 audio only.** The index describes building *Canis Canem Edit* PS2 RSTM `.RSM` files and names MFAudio and/or PS2STR as external executable dependencies. Do not apply it to PC/Scholarship Edition without separate evidence. [Source](https://github.com/EdnessP/scripts/blob/main/bully/rstm_build.py)

- **Anniversary Edition is a separate format family.** The index lists Android/iOS `.MSH`/`.TEX` model/texture support and separate `.EFF`/`.MTL`/`.WDB`/`.XML` encryption/parse tools. Do not conflate these with PC/PS2/Wii/Xbox 360 formats or assume they help a Scholarship Edition mod.

## Practical selection checklist

1. Identify the exact game edition and platform from the source files, not just a filename.
2. Prefer read-only extraction first; compare extracted data and keep originals untouched.
3. Match byte order, archive variant, compression, split-body arguments, and script version to the exact source documentation.
4. Before rebuilding or running an in-place metadata updater, keep a separate backup and use a disposable copy.
5. Read the current tool source, dependencies, license, and any notices before installing or redistributing it; this bundle summarizes links and does not include the third-party scripts themselves.
6. Report which format/tool version was used and distinguish a successful extraction/build from a verified in-game result.
