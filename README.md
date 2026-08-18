# repository-entity-store

Side 5 of the hexagon: an interface that gets, creates and changes entities. This one gets,
creates and changes a 100-byte entity over the iceoryx2 ring `transport-ingest-python`
already opens.

**Hello world.** The environment resolves and the generated codec is here; the repository
itself is not written yet. `pixi.toml` names the tasks it will answer to — `check`, `selftest`
and `serve` — and none of the three has a module behind it. That is stated rather than
implied, because a skeleton that reads as finished is worse than an empty directory.

## What is here

| | |
| --- | --- |
| `pixi.toml` | the environment, pinned to what `transport-ingest-python` pins |
| `gen/xr_grid_entity_packet.py` | the generated 100-byte entity codec |
| `entity_store/` | the package the repository will live in |

## Why the pins are exact

iceoryx2 is shared memory, so a repository and the interactor holding it are two processes on
one machine rather than two machines. Both ends must be the *same* iceoryx2: the service
registry rejects a second port whose type disagrees, and nothing checks that two versions lay
a slice out alike. The Python minor is pinned for the same reason — `Bus` is imported from
this environment, so a split would run that module on an interpreter it was never resolved
against.

`conformance.py` is meant to assert those pins equal `transport-ingest-python`'s rather than
trusting them. It is one of the three things not written.

## State

**Not built.** It entered the manifest on 2026-08-18, having existed as an untracked directory
in the workspace with no git repository behind it and nothing backing it up.
