# Game API, IDs, data and verification

## Exact API lookup (mandatory)
The community repository separates the *game's native global functions* from *DSL-added/overridden functions*. Search the correct index, then inspect the exact function page at the pinned revision. Each page may state a description, signature, params, return values, version and examples—but many are placeholders (`...`). The page filename/index entry alone is not enough. Never synthesize a signature, argument order, return type, enum value, or version.

- [Game global-function index](https://github.com/RanggaBS/bully-scripting/tree/65e8cf4617eee8d88010310e547b16c33f536cf4/docs/01-game-reference/global-functions)
- [DSL global-function index](https://github.com/RanggaBS/bully-scripting/blob/65e8cf4617eee8d88010310e547b16c33f536cf4/docs/02-dsl-reference/global-functions/01-all.md)
- [Scripting enumerations](https://github.com/RanggaBS/bully-scripting/tree/65e8cf4617eee8d88010310e547b16c33f536cf4/docs/01-game-reference/scripting-enumeration)
- [Object/model references](https://github.com/RanggaBS/bully-scripting/tree/65e8cf4617eee8d88010310e547b16c33f536cf4/docs/01-game-reference/object-models)

Use `search_files` on the local pinned source mirror when available; otherwise use `web_search`/`web_extract` against the pinned repository URLs. Capture the path/commit and what was actually found. When the page is incomplete, use a local test and another attributable source; otherwise mark it unknown and ask the user before speculative changes.

A concrete stub example: the supplied [Vercel page for `SetArrestRestartPointCameraPos`](https://bully-scripting.vercel.app/docs/game-reference/global-functions/SetArrestRestartPointCameraPos) shows `...` for its description, parameters, return values, and example, with only a generic `param1, ...` signature; the linked [repository `main` page](https://github.com/RanggaBS/bully-scripting/blob/main/docs/01-game-reference/global-functions/SetArrestRestartPointCameraPos.md) is likewise a stub. In the pinned local snapshot, the related `AddArrestRestartPoint`, `SetDefaultArrestRestartCameraPos`, and `RemoveArrestRestartPoint` pages are stubs too. Do not infer camera coordinates, argument order, or behavior from these function names; these pages establish no usable call recipe.

For current DSL/DSS APIs, also consult the maintainer's [DSL & DSS Functions catalog](https://www.nexusmods.com/bullyscholarshipedition/articles/55). The pinned GitHub index is older than the currently listed v16 release; see `references/current-dsl16-and-api.md` for precedence and the `(*)` undocumented marker.

The upstream docs include control/button codes, days, languages, factions, ped attitudes/emotions/stats, physical states, weather, blip icons/coronas, class indices, mission index, and model lists for objects, peds, vehicles, weapons, animations, textures and related categories. Game and PS2 model folders are separate; do not mix IDs across editions. Certain raw dumps include mesh hashes, point lists, triggers, sound/effect names, global variables/functions, and control codes. These are reverse-engineered community data, not official guaranteed API contracts.

Some entries are explicitly hazardous: mission index has dummy missions labeled “DO NOT RUN”; pool resizing documentation warns of instability. Do not experiment with such entries in a primary save. Use a backup/test save and a reversible mod-loader setup.

## Mod types and asset handling
A DSL collection can register certain game files into a temporary IMG archive via config entries (ACT, cutscene, trigger, IDE, scripts, world files, per the DSL config reference). That is not the same as a generic permission to modify arbitrary archives. For other assets, identify the exact PC loader/VFS and its version; preserve originals and use a non-destructive overlay/backup. Avoid distributing copyrighted game assets; distribute only original code/assets or files the user has rights to redistribute.

## Test matrix
- Static: Lua syntax/parser supported by the installed DSL; check collection config parsing/version and paths.
- Runtime: launch clean game with only target collection, inspect console; confirm readiness, feature behavior, no repeated errors, no unexpected performance impact.
- Lifecycle: stop/restart, load another mission/area, save/load if relevant, remove mod and confirm original behavior.
- Compatibility: exact game build, OS, DSL release, other mods and loader ordering.
- Safety: original files untouched, test save restored, no networking/system access unless explicitly required.

No static check alone proves in-game behavior. If the game isn't installed or the agent cannot launch it, state that runtime tests remain for the owner.
