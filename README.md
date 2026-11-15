# Bully: Scholarship Edition modding skill package

This package contains the Hermes skill `bully-se-modding`, its curated working references, and an offline snapshot of the community `RanggaBS/bully-scripting` documentation. It also points agents to the current DSL/DSS v16 Nexus function catalog and SimonBestia's format/model/action-tree documentation. Those external sources are linked and summarized with attribution rather than copied wholesale.

## Use in Hermes
- For this profile, the skill is installed at `skills/gaming/bully-se-modding`.
- To make another Hermes agent use it, copy the `bully-se-modding` directory into that agent's own profile `skills/gaming/` directory. Profiles are separate; this package does not modify other agents.
- Start a fresh agent session so it discovers the copied skill.
- The `sources/bully-scripting/docs/` directory is the pinned offline reference snapshot. For a smaller online-only install, copy `SKILL.md` and `references/` but omit `sources/`; the skill also links to the pinned online source. Keep `sources/` beside the skill when you need offline lookup.

## Important limitation
At the pinned community-docs revision, a text audit found a standalone `...` placeholder in 1,652 of 1,745 game-function Markdown pages and 147 of 329 DSL-function pages. Those are placeholder *page* counts—not counts of missing or unsupported functions—and the denominators include index pages, so the remaining 93/182 are not all complete function descriptions. The upstream introduction says the docs are still barebones. The skill therefore adds current DSL/DSS v16 links and broader asset-format references, and directs agents not to guess where the docs still lack detail. It does not include game binaries, DSL executables, third-party game assets, or test a mod in-game.

## Source and license
The upstream snapshot comes from `RanggaBS/bully-scripting` at commit `65e8cf4617eee8d88010310e547b16c33f536cf4`. Its `LICENSE` file is included with the source snapshot; preserve it when redistributing those upstream docs. Current DSL/DSS documentation and additional community asset references are linked and summarized, with attribution and their license boundaries documented in `THIRD_PARTY_SOURCES.md`. The upstream MIT license does not grant rights to Bully game content or third-party assets.
