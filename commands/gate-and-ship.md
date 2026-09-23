---
description: "Quality gates then ship - runs /prepare-delivery then /ship in one command. Use after completing implementation to go from code to merged PR."
codex-description: 'Use when user asks to "gate and ship", "review and ship", "quality gates and ship", "prepare and ship", or wants to go from finished implementation to merged PR in one step.'
argument-hint: "[--base=BRANCH] [--skip-review] [--skip-docs]"
allowed-tools: Bash(git:*), Bash(gh:*), Bash(npm:*), Bash(node:*), Read, Write, Edit, Glob, Grep, Task, Skill, AskUserQuestion
---

# /gate-and-ship

Take a finished branch through the quality gates and, only if they pass, ship it: `/prepare-delivery`, then `/ship`.

Arguments: `$ARGUMENTS`

- `--base=BRANCH`: base branch for the gates and the PR target. Default: the remote default branch, else `main`.
- `--skip-review`: skip the review loop in the gates.
- `--skip-docs`: skip docs sync in the gates.

## Gates

Run the `prepare-delivery:prepare-delivery` skill with all the arguments. It ends with a `=== PREPARE_DELIVERY_RESULT ===` block. If the Skill tool is missing, read the prepare-delivery plugin's `skills/prepare-delivery/SKILL.md` and run it inline.

Ship only when `readyToShip` is true. Otherwise stop, show the gate report and the fix instructions, and tell the user to fix and run `/gate-and-ship` again. Shipping a branch the gates rejected is the one outcome this command exists to prevent.

## Ship

Run the `ship:ship` skill with:

- `--base <BRANCH>` when `--base=BRANCH` was given (ship takes the value as a separate word).
- `--state-file <path>` when `{stateDir}/flow.json` exists and its `git.branch` is the current branch. The gates just wrote it, and it tells ship that review, deslop and docs already ran, so it skips its own review pass. A flow for another branch belongs to someone else's `/next-task` run: do not pass it. `{stateDir}` is `$AI_STATE_DIR` when set, else `.opencode`, `.codex` or `.claude` at the repo root, whichever the gates wrote to.

If ship is not installed, stop after the gates, say the branch is ready, and suggest `/ship` or opening the PR by hand.

## Done

Either the gates rejected the branch and the user has the reasons, or ship ran and its report is the last thing in the reply. Report which step failed if one did, and that `/prepare-delivery` and `/ship` can be run on their own.
