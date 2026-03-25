# gate-and-ship

> Quality gates then ship - chains /prepare-delivery and /ship

## Commands

- **gate-and-ship** [--base=BRANCH] [--skip-review] [--skip-docs] - runs /prepare-delivery quality gates then /ship for PR + merge

## Critical Rules

1. **Plain text output** - Use `[OK]`, `[ERROR]`, `[WARN]`, `[CRITICAL]` for status markers.
2. **Only create necessary files** - Keep the working tree clean, only deliverables and tests.
3. **Task is not done until tests pass** - Delegated to prepare-delivery's delivery-validator.
4. **Create PRs for non-trivial changes** - Handled by ship:ship.
5. **Always run git hooks** - Verify hooks are installed before push.
6. **Use single dash for em-dashes** - In prose, use ` - ` (single dash with spaces).
7. **Report script failures with exact error output** - Diagnose before attempting workarounds.
8. **Token efficiency** - Save tokens over decorations.

## Cross-Plugin Dependencies

| Step | Plugin | Command/Skill |
|------|--------|---------------|
| Quality gates | prepare-delivery | `prepare-delivery:prepare-delivery` |
| Ship | ship | `ship:ship` |

## Stateless Plugin

This plugin is stateless - it delegates all state management to prepare-delivery and ship. No agents, no skills, one command.

## References

- Part of the [agentsys](https://github.com/agent-sh/agentsys) ecosystem
- https://agentskills.io
