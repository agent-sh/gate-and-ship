# gate-and-ship

> Quality gates then ship - chains /prepare-delivery and /ship

## Overview

One command, no agents, no skills, no state of its own. `/gate-and-ship [--base=BRANCH] [--skip-review] [--skip-docs]` runs the prepare-delivery quality gates and, only when they report `readyToShip`, runs ship for the PR and merge. State lives in those two plugins.

| Step | Plugin | Skill |
|------|--------|-------|
| Quality gates | prepare-delivery | `prepare-delivery:prepare-delivery` |
| Ship | ship | `ship:ship` |

The command reads the `=== PREPARE_DELIVERY_RESULT ===` block from prepare-delivery and passes `--base` and `--state-file` to ship, so a change to either plugin's interface needs a matching change here.

## Checks

No tests or CI in this repo. Run `agnix .` after editing the command or this file.

## Conventions

- Output is plain text with the status markers `[OK]`, `[ERROR]`, `[WARN]`, `[CRITICAL]`.
- In prose, write a spaced single dash (` - `), not ` -- ` or an em dash.
- Keep the working tree to deliverables; tests run in prepare-delivery's validator.
- When a step fails, report its exact error output and diagnose before working around it.

## References

- Part of the [agentsys](https://github.com/agent-sh/agentsys) ecosystem
- https://agentskills.io
