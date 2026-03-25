# gate-and-ship

Quality gates then ship - chains `/prepare-delivery` and `/ship` in one command.

Part of the [agentsys](https://github.com/agent-sh/agentsys) ecosystem.

## Installation

```bash
# Via agentsys (recommended)
claude plugin marketplace add agent-sh/agentsys

# Standalone
claude mcp add-json gate-and-ship '{"type":"url","url":"https://github.com/agent-sh/gate-and-ship.git"}'
```

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

If Step 1 fails, Step 2 does not run.

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
