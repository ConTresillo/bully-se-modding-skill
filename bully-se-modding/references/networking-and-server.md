# DSL networking and script server

## Scope
Derpy's Script Server is a separate server-side component. Upstream says it can start/stop collections, send client scripts/files, run server scripts with many DSL functions, and exchange arbitrary Lua values through network events. It explicitly says DSL/the server does **not itself synchronize game state**. Do not describe a network script as multiplayer gameplay sync unless the mod implements and tests that behavior.

## Client script/config behavior
Server collection config can declare `client_script` and `client_file`; these are sent to players when a collection runs/restarts. On connection, player local collections stop unless `allow_on_server` permits them; server collections then start using the sent files. The full collection config is transmitted to clients. Therefore never put secrets, private IPs, credentials, or server-only allowlists in a collection config or a file marked for client transfer. Keep private server configuration in a separate server-only file.

## Event trust boundaries
Use documented `RegisterNetworkEventHandler` and `SendNetworkEvent` APIs; namespace event names (`mod_name:event`) to avoid collisions. Network events are activated by the opposite side. Treat client-originated event arguments as untrusted: validate types, lengths, ranges, permissions, rate, and current state before acting. Server can rely only on the first event argument being a valid connected player ID, according to the docs. Keep server authority over state; clients should request actions, not assert outcomes.

Local server events originate from the server and are distinct from network events. Player IDs may be reused after disconnect; clear references on `PlayerDropped`. The docs distinguish invalid, valid, and connected player states; check current validity before sending or mutating.

## State synchronization (current-version check)
The older community network overview says state sync is not automatic. The current DSL/DSS v16 API catalog lists explicit Sync APIs. Read the current article and installed readme for side/version details; do not treat a transport event as state synchronization. Design authority and replication explicitly, validate ownership/lifecycle, and test with a dedicated server/client setup before claiming synchronized gameplay.

- Events use namespaced identifiers and small serializable payloads.
- Authenticate/authorize every action on server; validate even though DSL provides an event handler.
- Bound message sizes, action frequency, and expensive work.
- Clear player/session references during disconnect and collection shutdown.
- Do not assume DSL provides state sync, encryption, anti-cheat, durable accounts, or safe public hosting; verify each separately.
- Do not open firewall ports, expose a server, or deploy account/admin scripts without owner permission. Treat sample server manual values as historical, not current configuration.

Primary sources:
- [Network scripting](https://github.com/RanggaBS/bully-scripting/blob/65e8cf4617eee8d88010310e547b16c33f536cf4/docs/02-dsl-reference/basic-concepts/04-network-scripting.md)
- [DSL overview](https://github.com/RanggaBS/bully-scripting/blob/65e8cf4617eee8d88010310e547b16c33f536cf4/docs/02-dsl-reference/basic-concepts/01-about-dsl.md)
- [Server manual](https://github.com/RanggaBS/bully-scripting/blob/65e8cf4617eee8d88010310e547b16c33f536cf4/docs/03-miscellaneous/resources/dsl-server-manual.md)
- [RegisterNetworkEventHandler reference](https://github.com/RanggaBS/bully-scripting/blob/65e8cf4617eee8d88010310e547b16c33f536cf4/docs/02-dsl-reference/global-functions/RegisterNetworkEventHandler.md)
