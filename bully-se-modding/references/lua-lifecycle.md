# Lua lifecycle, threads, state and drawing

## Script lifecycle
The community DSL guide describes optional `gamemain`, `MissionSetup`, `main`, and `MissionCleanup` functions. `gamemain` runs immediately after scripts initialize and can receive an early update. `MissionSetup` runs on script start; an error there shuts down the script. `main` follows setup (or starts immediately if setup is absent). `MissionCleanup` runs during shutdown. Cleanup threads keep the script/collection in a stopping state until they finish; threads they create are also cleanup threads. Keep cleanup bounded and reliable.

Each DSL script gets its own environment. `GetScriptSharedTable()` shares a table across scripts in a collection. The game's `shared` table and `_G` have broader visibility; avoid polluting globals. DSL docs describe `dsl` as cross-collection shared tables and `net` as network-script tables; do not assign to the `dsl`/`net` namespace itself. Check precise DSL version and APIs.

## Readiness and thread scheduling
The DSL overview tells new scripts to wait until `SystemIsReady()` is true before most game calls to avoid crashes. Guard all delayed entity access again because a ped/object may have been deleted while waiting.

The DSL `CreateThread` replaces the base game function while DSL is active (unless `UseBaseGameScriptFunctions(true)` changes behavior). A string can name a function in the current environment; extra arguments are passed through. The thread is attached to the current script. Use documented DSL thread types/functions for other timing phases:
- `GAME`: after normal game scripts.
- `SYSTEM`: each frame before other work/input.
- `DRAWING`: just before presentation.
- DSL 4+: `POST_WORLD` after world before HUD; `PRE_FADE` before camera fade.
- DSL 6+: `GAME2` after ordinary `GAME` threads.
- DSL 8+: `PRE_GAME` before ordinary `GAME` threads.

Use per-frame loops only when needed, yield with the documented `Wait`, and keep CPU work bounded. Do not assume the function's actual wait units/semantics from its name: many function reference pages are placeholders. Check the pinned function page and local loader/API before relying on it.

## Compatibility and cleanup
The DSL guide notes that most native game functions work, but some script-pool-sensitive behavior may differ. It specifically warns about button-sequence functions and notes `BlipAddXYZ` may not create a ground blip by default in DSL. Compatibility helpers such as `CallFunctionFromScript` exist for certain cases. Verify the exact helper doc (and whether that page is complete); if uncertain, use the conservative base-game script replacement path or mark behavior unverified.

At shutdown: stop/detach event handlers, terminate owned threads through documented methods, restore temporary input/mission/timecycle/entity changes, flush/close opened handles, and avoid cleanup code that can wait forever. Test stop → restart → reload.

## Rendering
The DSL rendering guide states normalized coordinates: `(0,0)` top-left, `(1,1)` bottom-right; sizes are fractions of screen size. Use aspect-ratio functions where a layout must keep physical dimensions or texture proportions. Colors/alpha are 0–255. Text formatting calls affect the next draw/measure; discard/pop formatting when abandoning a pending draw. Drawing is physically performed in `DRAWING`, `POST_WORLD`, or `PRE_FADE` threads; other thread calls are cached until the chosen draw layer executes. Confirm every drawing function's exact arguments in its page.

Primary sources:
- [Scripts and threads](https://github.com/RanggaBS/bully-scripting/blob/65e8cf4617eee8d88010310e547b16c33f536cf4/docs/02-dsl-reference/basic-concepts/03-scripts.md)
- [Global tables](https://github.com/RanggaBS/bully-scripting/blob/65e8cf4617eee8d88010310e547b16c33f536cf4/docs/02-dsl-reference/basic-concepts/08-global-variables.md)
- [Render functions](https://github.com/RanggaBS/bully-scripting/blob/65e8cf4617eee8d88010310e547b16c33f536cf4/docs/02-dsl-reference/basic-concepts/07-render-functions.md)
- [Relative paths and safety](https://github.com/RanggaBS/bully-scripting/blob/65e8cf4617eee8d88010310e547b16c33f536cf4/docs/02-dsl-reference/basic-concepts/05-relative-paths.md)
