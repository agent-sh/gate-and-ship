# gate-and-ship

Quality gates then ship - chains `/prepare-delivery` and `/ship` in one command.

Part of the [agentsys](https://github.com/agent-sh/agentsys) ecosystem.

## Installation

```bash
agentsys install gate-and-ship
```

Or add the marketplace in Claude Code with `claude plugin marketplace add agent-sh/agentsys` and install `gate-and-ship` from it.

## Usage

```bash
/gate-and-ship                       # Full: quality gates + ship
/gate-and-ship --skip-review         # Skip review, still ship
/gate-and-ship --skip-docs           # Skip docs sync
/gate-and-ship --base=develop        # Against a specific base branch
```

## What It Does

```
/gate-and-ship = /prepare-delivery + /ship
```

**Step 1** - Runs `/prepare-delivery` (all quality gates: deslop, simplify, review loop, validation, docs sync)

**Step 2** - Runs `/ship` (PR creation, CI monitoring, merge)

`--base` is forwarded to both steps. `--skip-review` and `--skip-docs` are forwarded to Step 1 only.

Step 2 runs only when Step 1 reports `readyToShip`. When the gates wrote a flow state for the current branch, it is passed to `/ship` as `--state-file`, so ship does not run a second internal review. A flow state from another branch is never passed. Without the ship plugin, the command stops after the gates.

## Composability

Each piece runs independently:

| Command | Use when |
|---------|----------|
| `/prepare-delivery` | Want to review before deciding to ship |
| `/ship` | Already validated, just ship it |
| `/gate-and-ship` | Do both in sequence |

## Dependencies

- [prepare-delivery](https://github.com/agent-sh/prepare-delivery) - quality gates
- [ship](https://github.com/agent-sh/ship) - PR + CI + merge

## Platforms

Works with Claude Code, OpenCode, Codex CLI, and Cursor via agentsys.

## License

MIT
