# Changelog

## [Unreleased]

### Changed
- AGENTS.md trimmed for current models: dropped the GPU validation text and the rules that only restated what prepare-delivery and ship handle, added an Overview with the interface this command depends on, and named `agnix .` as the check. The command is unchanged; it was rewritten for current models in 0.2.0.

## [0.2.0] - 2026-09-24

### Changed
- Rewrote /gate-and-ship for current models: the two steps, the ship condition and the defaults in prose, instead of JavaScript for the model to act out.

### Fixed
- Ship ran whenever the prepare-delivery skill returned, with no check of its result. It now runs only when the gates report `readyToShip`.
- Any `flow.json` in the state dir was passed to /ship as `--state-file`, including one left by another branch's /next-task run. Ship trusts that file to skip its review and clean up a task, so only a flow owned by the current branch is passed now.
- README install line used `claude mcp add-json`, which registers an MCP server, not a plugin.

## [0.1.0] - 2026-03-25

### Added
- Initial release - orchestrator that chains /prepare-delivery then /ship
- /gate-and-ship command
- Forwards --base, --skip-review, --skip-docs flags
