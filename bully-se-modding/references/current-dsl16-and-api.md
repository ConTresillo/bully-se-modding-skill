# Current DSL/DSS release and API source

## Current release check
The official-by-author Nexus page for [derpy's script loader](https://www.nexusmods.com/bullyscholarshipedition/mods/43) currently lists **Version 16** (the page's update history/posts report 16 released on 12 Oct 2026). Re-check the live page and the installed release's `readme.txt` at the start of a project; this changes over time. DSL 16 has separate S and Full packages. The page says S excludes system-access features; Full has optional system access. Never tell a user to enable system access or download an untrusted binary. Use the official page and verify the readme, archive signature/provenance and loader version before install.

The primary current catalog is the maintainer's [DSL & DSS Functions](https://www.nexusmods.com/bullyscholarshipedition/articles/55) article. It organizes signatures by category and marks undocumented functions with `(*)`; it distinguishes `[CLIENT]`, `[SERVER]`, `[SHARED]`, and `[SYSTEM]`. Treat it as an API index, not a full semantic manual: it explicitly notes that some functions are not documented yet. Check `readme.txt`/release notes for behavior not specified there; use actual runtime tests where safe.

## Precedence rules
1. Installed DSL/DSS v16 release readme and current maintainer article for current supported function names, roles and version requirements.
2. DSL docs repo at commit `65e8cf4617eee8d88010310e547b16c33f536cf4` for older collection/config/lifecycle/render/network explanations, reference lists, and specific function-page details—verify any version claim against current release docs.
3. Other community tutorials/references as secondary corroboration, with author/date/platform/version noted.
4. Historical forum posts, decompiled-script lists, and reverse-engineered dumps are leads only—not authoritative contracts.

If sources conflict, don't silently choose the most convenient one. Record the conflict, prefer current maintainer docs for version/API availability, and test locally where possible.

## API discovery steps
- Look up the function in article 55 and record its side tag and exact signature; do not copy a `[SYSTEM]` API into an ordinary script.
- Search the v16 release readme and any current docs for detailed parameter units, return values, errors, and lifecycle constraints.
- If the only article entry is marked `(*)`, do not infer arguments from its name. Search a pinned community example or an in-game test in a disposable setup, then label the result as observation/inference.
- Check `DSL` versus `DSS`, client versus server, and `S` versus `Full` capabilities before using the function.
- Preserve the package's original files and config; test a minimal isolated script before adding a function to a larger mod.

## DSL v16 API families observed in the current catalog
The article lists camera, command/config, console/content, events, files, hooks, input, localization, manager/lifecycle, matrices/vectors, memory/system, miscellaneous, model overrides, networking, objects, peds, pools, projectiles, rendering, save data, serialization, sync, timecycle/weather, and vehicle functions. The list is broad, but its `(*)` marker means the full behavior contract is not documented there. Do not describe all functions as safe or available on all builds.

The current catalog includes explicit Sync APIs, unlike the older network overview's emphasis that the server does not synchronize game state automatically. The safe interpretation is: synchronization is not implicit; the current API offers explicit sync mechanisms that a mod must implement correctly and test. Validate ownership, authority, lifecycle and payloads.

## Version compatibility
The pinned GitHub function index says 327 DSL globals and includes a DSL 11 “Not released yet” note. This is plainly older than the current v16 Nexus release. Do not use its DSL 10 labels as the present maximum, and do not map a feature's minimum version solely from that old index. Verify with the current release readme/article and target installation.
