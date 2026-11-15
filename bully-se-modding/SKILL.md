---
name: bully-se-modding
description: Use when making Lua mods for Bully Scholarship Edition.
version: 0.1.0
author: ConTresillo, Hermes Agent
license: MIT
platforms: [windows, linux, macos]
metadata:
  hermes:
    tags: [Bully, Scholarship Edition, DSL, Lua, game-modding]
    related_skills: [test-driven-development, systematic-debugging]
---

# Bully: Scholarship Edition Modding
Use the community Bully Scripting Docs and Derpy Script Loader (DSL) references to author, inspect, package, and debug PC mods. This is an evidence-driven guide, not a claim that the upstream docs are complete; check the exact loader/game version and confirm every API against its primary reference before relying on it.

## When to Use
- Create, review, debug, or package a Bully: Scholarship Edition PC Lua script/DSL collection.
- Inspect game scripting functions, enums, model IDs, events, or DSL server/client behavior.
- Do not assume this covers console editions, arbitrary binary patching, or rights to redistribute game assets.

## Prerequisites
- Confirm the user's platform, Bully: Scholarship Edition build, DSL version, and intended mod type (DSL Lua collection, network script, base-game script replacement, or asset/archive mod).
- Use the installed game and DSL readme as authoritative for installation. Never download a game, executable, paid asset, or arbitrary binary without authorization.
- Primary source: `https://github.com/RanggaBS/bully-scripting/tree/65e8cf4617eee8d88010310e547b16c33f536cf4` (community-maintained, MIT; see `references/source-map-and-coverage.md`). It is an older snapshot, not the current DSL release manual.
- Current release and DSL/DSS API list: [Nexus DSL page](https://www.nexusmods.com/bullyscholarshipedition/mods/43) and its [DSL & DSS Functions article](https://www.nexusmods.com/bullyscholarshipedition/articles/55). Read the matching package `readme.txt` and live documentation before relying on current behavior.


## Procedure
1. **Scope/version gate.** Identify the exact PC game build and DSL/DSS version. The release page currently lists v16; verify it live and inspect the installed loader's readme. The pinned community GitHub docs cover an older DSL-era snapshot, so never infer current compatibility from their DSL 10/11 notes. For each API, require the installed version to satisfy the current DSL & DSS Functions article and package readme.

2. **Inspect before coding.** Read `references/quickstart-and-loader.md` and the relevant topic reference. Search the pinned upstream source for the exact function page, enum, or object ID. The source function indexes contain many placeholder pages; check the page body, not just its existence or index entry. If a page is a stub, say so and seek a second primary/community reference or a local runtime check—never invent a signature.
3. **Pick the least invasive format.** Prefer a DSL script collection for new Lua behavior. Use an existing script replacement or registered game file only when the task requires changing a base-game asset/script. Keep original game files untouched; recommend a backup and a reversible loader/VFS workflow.
4. **Design the mod.** Define a concise behavior spec, collection ID/name, dependencies and minimum DSL version, lifecycle/thread plan, configuration keys, cleanup behavior, and failure/compatibility limits. Keep features in small files/modules with namespaced globals/events; avoid global monkey patches unless necessary and explicitly documented.
5. **Implement with safe lifecycle.** For ordinary gameplay calls, follow the source's readiness guidance (`SystemIsReady`) and wait for valid entities after delays. Keep per-frame work bounded; yield using documented thread APIs. Make cleanup stop spawned threads/events and restore state. Read exact function docs for parameter/return semantics and nil/error behavior.
6. **Test.** Use the real DSL/game when available: load one collection, inspect the DSL console, exercise normal/error/shutdown/restart paths, check logs, and verify no base files changed. Static checks or Lua parsers are useful but do not prove game integration. If game/DSL is missing, report tests as unrun and provide exact user verification steps. Do not claim in-game verification from source inspection alone.
7. **Package.** Deliver a folder or root-level ZIP collection with its config and scripts at archive root; include README, tested game/DSL version, install/remove steps, permissions/system-access needs, dependencies, and known limits. Keep licensed third-party assets separate and obtain permission before redistribution.
8. **Record evidence.** Report changed files, source pages consulted, game/DSL version, tests actually run, packaging, and unresolved uncertainty. Separate confirmed facts from hypotheses.

## Pitfalls
- The pinned GitHub docs explicitly describe themselves as work in progress. At revision `65e8cf4`, 1,652 of 1,745 game-function pages and 147 of 329 DSL-function pages contain a standalone `...` placeholder. Those are file counts, not counts of missing functions; some non-placeholder pages are indexes or progress notes. The GitHub DSL index is stale (its own text says DSL 11 is unreleased), while the current Nexus release page lists DSL/DSS v16. Use the GitHub snapshot for its rich older guides/data, but use the live Nexus article + installed readme for current APIs and version requirements. The current function article itself marks some entries undocumented; when neither source details behavior, verify in a local game/loader or state the gap—never fill it by guessing.

- The community docs say Bully uses Lua 5.0.2; do not assume modern Lua syntax/libraries or standard Lua binaries are compatible without checking the installed DSL/readme.
- DSL/DSS is not automatic game-state sync: the current v16 function catalog exposes explicit Sync APIs, so agents may use those only after checking the current article/readme and testing the exact server/client roles. Validate every client-originated event and never claim unsupported synchronization.

- DSL may permit powerful Lua/system access in some builds. Keep system access disabled unless the user explicitly needs it; prefer safe relative file APIs. The source warns that non-S builds may trigger antivirus. Never disable antivirus or weaken security controls to make a mod run.
- Never use undocumented raw pointers, pool resizing, binary patching, or mission indices in a live save without a reversible test setup and explicit warning; source material itself marks some pools/mission entries experimental or “do not run.”
- Avoid adding network listeners, opening firewall ports, starting server processes, overwriting saves, or modifying game installation files without user authorization.

## Verification
- Confirm the collection's root/config/script layout and minimum DSL version against the pinned docs and installed readme.
- Search every game/DSL API call in the relevant source page; if it is a stub, mark the API unverified.
- Run static/Lua checks where available, then test in an isolated copy/test save when possible; verify graceful stop/restart and clean removal.
- List separately: source-grounded checks, static checks, in-game checks, and anything not tested.

## References
Load only the linked reference needed for the current task:
- `references/quickstart-and-loader.md` — installation boundary, collection layout, config and startup.
- `references/lua-lifecycle.md` — script lifecycle, threads, readiness, shared state, rendering.
- `references/networking-and-server.md` — client/server model, events, trust boundaries.
- `references/game-api-and-data.md` — API lookup, enums, models, assets and test approach.
- `references/current-dsl16-and-api.md` — current release/API sources and conflict resolution.
- `references/native-script-and-assets.md` — native scripts, archives, model/action-tree data, platform/risk boundaries.
- `references/source-map-and-coverage.md` — all source owners, source dates/commits, license boundaries and coverage gaps.
