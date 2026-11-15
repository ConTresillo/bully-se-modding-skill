# Quick start and loader workflow

## Source-grounded facts
- Bully: Scholarship Edition PC scripting uses Lua; the community docs say the game uses Lua 5.0.2, configured with a 4-byte `LUA_NUMBER`, with additional differences. Verify on the installed DSL release before using syntax or libraries.
- Derpy Script Loader (DSL) is a community loader for PC. The docs say scripts can run as source `.lua`; consult the installed DSL `readme.txt` for actual installation, security/config, and version details.
- A script collection is the mod unit. Collections may be a folder (“normal”), a standalone `.lua`/`.lur` script, or a ZIP (“zipped”); support for zipped collections starts at DSL 4. Collections can be organized in `[CATEGORY]` folders for the end user, but release collections should normally sit at the scripts root.
- For a ZIP, place the *contents* of the collection at the ZIP root. Do not wrap them in an extra collection-name directory, or `config.txt`/entry scripts may not be found.
- The collection normally belongs under `_derpy_script_loader/scripts`. Check installed readme for the actual game location and mod loader version.

## Suggested safe layout
```text
MyMod/
  config.txt
  main.lua
  scripts/             # optional modules, if referenced by the config/code
  README.md
```
Keep config and the main script at collection root unless the collection config explicitly points elsewhere. If the docs or the installed loader disagree, follow the installed version's readme and test.

## Collection config
The community config guide describes a simple line-oriented key/value format; keys are case-sensitive. DSL 5+ supports `key: value`, `key = value`, quoted strings, comments beginning `#` or `;`, and ignores section-like lines beginning `[`. Repeated keys can represent arrays and can be read through APIs such as `AllConfigValues`; check exact function docs.

Common collection fields documented upstream:
- `require_name`, `require_version`, `require_dependency` — declare requirements. Version requirements use an integer version only (for example, `7`, not `7.1`).
- `main_script` — gameplay entrypoint (default `main.lua`; if a `.lua` is absent DSL may try `.lur`, per docs).
- `init_script` — runs once at first main menu; game functions are unavailable at this stage.
- `pre_init_script` — very early; rendering/game functions unavailable.
- `auto_start` — collection preference, interacts with the global auto-start settings.
- `allow_on_server` — keep compatible local collections active when connected; intended for non-gameplay-altering mods.
- `act_file`, `cuts_file`, `trigger_file`, `ide_file`, `scripts_file`, `world_file` — registered game files in a temporary IMG archive for client collections; no effect on server scripts.
- custom key/value entries may be read by config functions.

The DSL v10 community guide says collection config files are no longer generated automatically, so create one deliberately for that release. Do not assume sample values or feature flags apply to every version. The live maintainer page lists DSL/DSS v16; follow its matching package readme for current requirements and collection behavior.


## Startup stages and console
`pre_init_script` runs at game start with no rendering/game calls; `init_script` runs when main menu is first reached, also before game functions are available; `main_script` runs after the game script manager is set up and before the game's `main.lur`. Collections can also start manually or as dependencies. DSL's global `dont_auto_start`, per-collection `auto_start`, and `force_auto_start_pref` interact; inspect the upstream collection guide before changing defaults.

The docs describe `/list`, `/check <collection>`, `/start <collection|*>`, `/restart <collection|*>`, and `/stop <collection|*>`. Stopping begins cleanup; it is not an immediate kill. Use the console output to investigate script/collection errors.

## Release checklist
1. Ensure config and entrypoint are in expected paths and the minimum DSL version is correct.
2. Build ZIP with config/script files at archive root; do not nest one extra directory.
3. Include install/update/uninstall steps, version tested, dependencies, known limitations, and any required file-registration permissions.
4. Keep an untouched original game directory and test using a copy/test save.

Primary source pages (pinned):
- [DSL overview](https://github.com/RanggaBS/bully-scripting/blob/65e8cf4617eee8d88010310e547b16c33f536cf4/docs/02-dsl-reference/basic-concepts/01-about-dsl.md)
- [Collections](https://github.com/RanggaBS/bully-scripting/blob/65e8cf4617eee8d88010310e547b16c33f536cf4/docs/02-dsl-reference/basic-concepts/02-collections.md)
- [Config files](https://github.com/RanggaBS/bully-scripting/blob/65e8cf4617eee8d88010310e547b16c33f536cf4/docs/02-dsl-reference/basic-concepts/06-config-files.md)
- [Loader downloads and safety note](https://github.com/RanggaBS/bully-scripting/blob/65e8cf4617eee8d88010310e547b16c33f536cf4/docs/03-miscellaneous/downloads/dsl.md)
