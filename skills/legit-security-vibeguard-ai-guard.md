---
name: Install and run Legit VibeGuard (AI Guard) in Claude Code
description: >-
  Install Legit Security's provider-published AI Guard plugin so an agent
  session is screened for secrets leakage, prompt injection, hidden characters,
  and disallowed MCP tools before every prompt and tool call.
api: null
operations: []
source: https://github.com/Legit-Labs/claude-marketplace
method: searched
generated: '2026-07-19'
---

# Legit VibeGuard (AI Guard) for Claude Code

Legit Security publishes this plugin itself. Every command and hook below is
taken verbatim from `Legit-Labs/claude-marketplace` — nothing is inferred.

## Prerequisites

- Claude Code CLI.
- A Legit Security account (https://www.legitsecurity.com).

## Install

1. Add the marketplace:

   ```
   /plugin marketplace add Legit-Labs/claude-marketplace
   ```

2. Install the plugin (`vibeguard-unix` for macOS/Linux, `vibeguard-windows`
   for Windows — both at version `0.1.245`):

   ```
   /plugin install vibeguard@legit-labs-claude-marketplace
   ```

3. Authenticate the bundled `legit` CLI against your account:

   ```bash
   legit auth
   ```

## What it enforces

| Control | Effect |
|---|---|
| Secrets detection | Blocks API keys, tokens and credentials from leaving in prompts |
| Prompt injection prevention | Blocks injection attempts before they reach the model |
| Hidden character detection | Catches invisible and homoglyph characters |
| MCP allow list enforcement | Restricts which MCP tools Claude Code may call |

## Where it runs

The plugin registers three Claude Code hooks (`hooks/hooks.json`):

- `SessionStart` → `vibeguard.sh claude-hook session-start` — validates config
  and connects to the Legit Security backend.
- `UserPromptSubmit` → `vibeguard.sh claude-hook user-prompt` (timeout 180s) —
  scans each prompt for secrets, hidden characters and injection.
- `PreToolUse` → `vibeguard.sh claude-hook before-tool-use` (timeout 180s) —
  enforces the MCP tool allow list.

When a threat is detected Claude Code is blocked from proceeding and the
operator is shown what was caught.

## Supported platforms

macOS (arm64, amd64), Linux (amd64, arm64), Windows (amd64, arm64).

## Support

support@legitsecurity.com
