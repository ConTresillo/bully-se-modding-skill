# Game-world and character reference: Harrington House

Use this note as a source-backed starting point, not a complete Bully encyclopedia. For other lore questions, search the exact topic and game edition online; distinguish official/game-script evidence from community wiki summaries and fanon. The community-wiki pages below summarize observed gameplay and are useful but not developer documentation.

## Harrington House: canon behavior

- Harrington House is a Preppy building on Bullworth Academy grounds. It can be entered in the missions **Weed Killer** and **Complete Mayhem**; free-roam access opens after Chapter V.
- The location page explicitly notes that Preppies are not seen inside outside missions. An empty interior during ordinary free roam is therefore expected behavior, not by itself a bug.
- **Weed Killer** (Chapter II, optional) is time-gated. The wiki lists 08:00–08:56, 11:33–12:56, and 15:33–23:00. It stages these occupants: Bif Taylor as doorman; Gord and Parker on the first floor; Tad and Justin on the second; Chad and Bryce near the top-floor greenhouse. During the exit phase, Preppies attack Jimmy.
- **Complete Mayhem** (Chapter V) stages Derby Harrington inside, with Chad Morris and Bryce Montrose guarding him during the riot.
- The courtyard also has Chad's dog Chester; do not mistake exterior NPC presence for an interior population schedule.

Sources:
- [Harrington House (Bully Wiki)](https://bully.fandom.com/wiki/Harrington_House)
- [Weed Killer (Bully Wiki)](https://bully.fandom.com/wiki/Weed_Killer)
- [Complete Mayhem (Bully Wiki)](https://bully.fandom.com/wiki/Complete_Mayhem)

These are community-maintained game-reference pages, not Rockstar documentation. Treat mission rosters/locations as corroborated gameplay descriptions; verify version differences if they matter.

## NPC/model references for a Preppy-population mod

The community [Bully LUA Reference index](https://derpy54320.github.io/Bully-LUA-Reference/index.html) organizes model IDs, scripting IDs, function docs and Lua 5.0.2 notes. Its [Model IDs → Peds table](https://derpy54320.github.io/Bully-LUA-Reference/model/peds.html) lists these model IDs and names in its PC-oriented table:

- `30` Gord (`PRH1_Gord`)
- `31` Tad (`PRH1a_Tad`)
- `32` Chad (`PRH2a_Chad`)
- `33` Bif (`PR2nd_Bif`)
- `34` Justin (`PRH3_Justin`)
- `35` Bryce (`PRH2_Bryce`)
- `37` Derby (`PRlead_Darby`; the table uses the spelling `Darby` in the model name)
- `40` Parker (`PRH3a_Parker`)

These IDs come from a community reference, not an official SDK. Check the target PC game build's model list and loader requirements before using them. Do not mix IDs from PS2/Anniversary/other-edition model tables. `DEFAULTPED` is specifically warned against because it can crash in that reference.

## Spawn API evidence and implementation boundary

The pinned `RanggaBS/bully-scripting` documentation describes native game function `PedCreateXYZ(id, x, y, z)`: it creates a character at coordinates, returns the created ped handle (not the model ID), and ties the ped to the current script so it is cleaned up when that script terminates. The docs also describe `PedCreatePoint(id, plist, pnumber)` for pre-defined points, requiring the relevant `.DAT` point list to be loaded. DSL's `PedCreateScriptless(model, x, y, z, heading)` was added in DSL 6 and deliberately is not attached to the current script; upstream says not to use it without a good reason.

- [`PedCreateXYZ` at pinned source commit `65e8cf4`](https://github.com/RanggaBS/bully-scripting/blob/65e8cf4617eee8d88010310e547b16c33f536cf4/docs/01-game-reference/global-functions/PedCreateXYZ.md)
- [`PedCreatePoint` at pinned source commit `65e8cf4`](https://github.com/RanggaBS/bully-scripting/blob/65e8cf4617eee8d88010310e547b16c33f536cf4/docs/01-game-reference/global-functions/PedCreatePoint.md)
- [`PedCreateScriptless` at pinned source commit `65e8cf4`](https://github.com/RanggaBS/bully-scripting/blob/65e8cf4617eee8d88010310e547b16c33f536cf4/docs/02-dsl-reference/global-functions/PedCreateScriptless.md)

This demonstrates that the scripting API has a documented mechanism for creating a ped at a location, but it does **not** prove that any guessed Harrington House coordinates, area/streaming hooks, collision, animation, AI routine, persistence, or NPC interactions will work. The pinned community docs are incomplete and older than the currently listed DSL/DSS release. For a Harrington House population mod:

1. First inspect mission scripts and level/point data or a trustworthy PC coordinate map to locate valid interior standing points. Do not invent coordinates from screenshots or convert coordinates from another edition.
2. Verify the current DSL release/readme and the exact API page for each function. Prefer script-owned NPCs with explicit teardown over unowned/persistent peds; prevent duplicate spawns when entering/re-entering the interior.
3. Use canon NPCs and sensible placements from the mission roster as design references, but make free-roam behavior configurable (e.g. small idle group, social conversations, optional security/party setup). Avoid spawning mission actors during a mission unless the mod deliberately detects and handles that state.
4. Test in the user's exact PC game/DSL version: load/unload, door transitions, repeated entry, NPC collisions/AI, save/load, mission start/exit, and clean mod removal. Source inspection alone is not an in-game test.

## Research procedure for other game-knowledge questions

Search current game references/walkthroughs for the specific edition, chapter, mission, character, location, or mechanic. Prefer game scripts or direct primary data for implementation details; use multiple independent gameplay references for lore claims when available. Cite sources in answers, label speculation, and do not confuse cut content, fanon, or modded behavior with canon. If the user asks for a mod but lacks the game/loader, explain which parts can be researched or statically built and which runtime checks remain impossible.
