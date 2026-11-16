# Source map, license and limits

## Primary source
- Project: [RanggaBS/bully-scripting](https://github.com/RanggaBS/bully-scripting)
- Description: fan-made/community Bully: Scholarship Edition PC scripting documentation; not an official Rockstar source and not affiliated with game developers.
- Published documentation site: [bully-scripting.vercel.app](https://bully-scripting.vercel.app), linked by the repository README. The README calls it the official documentation site for this scripting project; that does not make it official Rockstar documentation. Individual pages can still be incomplete or placeholders.
- Audited revision: `65e8cf4617eee8d88010310e547b16c33f536cf4` (main at audit time).
- License file in repository: MIT, copyright Rangga Buana Saputra (2025). If redistributing copied portions of the repository, include its copyright/license text. Do not imply this license covers Bully, DSL binaries, game content, or third-party assets.
- `docs/intro.md` explicitly says the documentation is barebones and missing functions, examples and general know-how. Treat it as a community reference, not complete truth.

## Audited source areas
- DSL overview/config/collections/scripts/network/render/relative-path/global tables: `docs/02-dsl-reference/basic-concepts/` (8 main concepts).
- Game API: `docs/01-game-reference/global-functions/` (1,745 Markdown files including indexes).
- DSL API: `docs/02-dsl-reference/global-functions/` (329 Markdown files including indexes; the index describes 327 functions).
- Enumerations: `docs/01-game-reference/scripting-enumeration/` (14 Markdown files).
- Object data: `docs/01-game-reference/object-models/` and `object-models-ps2/` (12 each; keep platform/version distinction).
- Other reference data: `docs/01-game-reference/raw-dumps/` (12 files; reverse-engineered data, use caution), downloads/resources including Lua info and DSL server manual.

## Completeness audit at the pinned revision
A count of function pages containing a standalone ellipsis placeholder found:
- Game functions: 1,652 of 1,745 pages have placeholder bodies; only 93 pages have no such placeholder (includes index/about pages, so fewer are full function docs).
- DSL functions: 147 of 329 pages have placeholder bodies; 182 have no standalone placeholder (includes index/progress pages).
These counts are a mechanical text audit, not a quality assessment. Other pages may still be incomplete, inaccurate, stale, or version-specific. The community's all-functions index lists 327 DSL globals and includes DSL 10-era features; its version history says DSL 11 is not released. Confirm the installed loader before using a listed feature.

## Exact source URLs
To retrieve any selected page, use its path at:
`https://github.com/RanggaBS/bully-scripting/blob/65e8cf4617eee8d88010310e547b16c33f536cf4/<source-path>`
For current upstream, inspect `main` separately and note its new commit SHA; do not silently replace the pinned baseline. In the full portable package, the exact source snapshot is included under `sources/bully-scripting/docs/`; if that folder is absent, use the pinned online links.

## Additional community sources audited
- Current maintainer release page: [DSL/DSS](https://www.nexusmods.com/bullyscholarshipedition/mods/43). It listed v16 at the time of this audit (page update 12 Oct 2026). Version and requirements change; re-check the page and the installed package readme.
- Current maintainer API catalog: [DSL & DSS Functions](https://www.nexusmods.com/bullyscholarshipedition/articles/55). It groups client/server/shared/system APIs and marks some entries `(*)` as not documented. Use it for current names/side/signature, not as a complete behavior contract.
- SimonBestia, [Bully Modding Documentation](https://github.com/SimonBestia/Bully-Modding-Documentation), audited commit `e14c2a85d5608aa205dca56a065044d8a90b7d19`. Its site says pages may be incomplete and permits reusing information with credit. No repo license was found in the inspected snapshot; this skill summarizes and links to the material, not copies the site.
- Kresenko, [Bully Modding part 1: Setup and first mod](https://kresenko.com/blog/bully-modding-part-1), dated 23 Feb 2025. A small beginner walkthrough using DSL's example and a console command; it is not an exhaustive manual and its config assumptions must be checked against the current DSL release.
- Snowypuppy, [Bully scripting global functions](https://snowypuppy.dev/bully/functions). This historical reference labels sources as C, DSL, Lua and standard-library functions and includes inferred/decompiled evidence; its own introduction says the page reflects an earlier update. Use only as secondary evidence; do not copy decompiled original scripts/assembly into the skill.
- `Razcoina/Bully-SE-scripts` is explicitly described as a decompilation project based partly on a pre-release debug build. It is excluded from the package; do not redistribute its game scripts/assets or treat that cross-edition material as a clean API specification.
- The 2011 Bully-Board “Ultimate Modding Thread” is an under-construction historical forum guide. Its archive/hex-edit procedures are low-confidence leads only, not safe default instructions.
- Bully Wiki pages hosted by Fandom: [Harrington House](https://bully.fandom.com/wiki/Harrington_House), [Weed Killer](https://bully.fandom.com/wiki/Weed_Killer), and [Complete Mayhem](https://bully.fandom.com/wiki/Complete_Mayhem). Used for paraphrased gameplay-location/mission roster facts in `game-world-and-characters.md`; community-maintained, not Rockstar-authored, and no substantial text/media is copied.
- Derpy54320, [Bully LUA Reference index](https://derpy54320.github.io/Bully-LUA-Reference/index.html) and [Peds model table](https://derpy54320.github.io/Bully-LUA-Reference/model/peds.html). Its listed PC-oriented Preppy model IDs are summarized in `game-world-and-characters.md`; secondary community reference, not an official SDK. Verify the exact game edition/build before use.
- EdnessP, [Tools & Plugins: Bully (Canis Canem Edit)](https://ednessp.github.io/tools#Bully_(Canis_Canem_Edit)) and linked scripts. Their archive/string/hash/audio/viewer capabilities are summarized in `community-bully-file-tools.md`; the site labels itself work in progress. Scripts are linked, not bundled, and their license terms were not established here. Verify each tool and platform before use.
- The [Bully Scripting Docs Vercel page for `SetArrestRestartPointCameraPos`](https://bully-scripting.vercel.app/docs/game-reference/global-functions/SetArrestRestartPointCameraPos) is a generated community-docs page. The page and corresponding repository `main` Markdown are placeholders (`...` for description/parameters/returns/example; generic signature), as are several adjacent arrest-restart functions in the pinned snapshot. This is an explicit example of why page existence is not evidence of an API contract.

## What this skill does not claim

- It is a curated procedure and source map, not an exhaustive rewrite of all 2,000+ reference files.
- It does not verify that any particular game/DSL version is installed or that a mod runs.
- It does not include game binaries or third-party assets.
- No MCP/game-control tool is included. A local game/loader or separate MCP server would need independent installation, source/security review and explicit setup.
- For undocumented APIs, use attributable evidence and runtime tests; if neither exists, stop and state the gap instead of guessing.
