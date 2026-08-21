# Awesome Claude Code Hooks [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of hooks, guides, tools, and examples for [Claude Code](https://docs.claude.com/en/docs/claude-code) hooks — the shell-command lifecycle events that let you intercept, block, log, or augment what your coding agent does.

Claude Code hooks fire on events like `PreToolUse`, `PostToolUse`, `SessionStart`, `SessionEnd`, `Notification`, `Stop`, and `UserPromptSubmit`, running arbitrary shell commands with structured JSON in/out. This list collects the best real-world implementations, so you don't have to write your security guardrail or notification hook from scratch.

Contributions welcome — see [CONTRIBUTING.md](CONTRIBUTING.md).

## Contents

- [Official Docs](#official-docs)
- [Getting Started / Guides](#getting-started--guides)
- [Security & Guardrail Hooks](#security--guardrail-hooks)
- [Notification Hooks](#notification-hooks)
- [Observability & Logging Hooks](#observability--logging-hooks)
- [Git & Commit Hooks](#git--commit-hooks)
- [Formatting / Linting / Testing Gates](#formatting--linting--testing-gates)
- [Voice / TTS Hooks](#voice--tts-hooks)
- [Session Memory & Context Hooks](#session-memory--context-hooks)
- [Frameworks & Toolkits (bundle many hooks)](#frameworks--toolkits-bundle-many-hooks)
- [Multi-Agent / Cross-Tool Hooks](#multi-agent--cross-tool-hooks)

## Official Docs

- [Claude Code Hooks Reference](https://docs.claude.com/en/docs/claude-code/hooks) — official event list, JSON schema, exit code semantics.
- [Claude Code Hooks Guide](https://docs.claude.com/en/docs/claude-code/hooks-guide) — official walkthrough with examples.

## Getting Started / Guides

- [disler/claude-code-hooks-mastery](https://github.com/disler/claude-code-hooks-mastery) — the most complete hands-on reference for every hook event, with working examples for each.
- [FlorianBruniaux/claude-code-ultimate-guide](https://github.com/FlorianBruniaux/claude-code-ultimate-guide) — 430K+ line guide covering hooks alongside skills, agents, and MCP.
- [ChrisWiles/claude-code-showcase](https://github.com/ChrisWiles/claude-code-showcase) — full project config example wiring hooks, skills, agents, and commands together.
- [diet103/claude-code-infrastructure-showcase](https://github.com/diet103/claude-code-infrastructure-showcase) — skill auto-activation + hooks + agents infrastructure example.

## Security & Guardrail Hooks

Hooks that block destructive commands, exfiltration attempts, or unsafe file access before they execute.

- [dwarvesf/claude-guardrails](https://github.com/dwarvesf/claude-guardrails) — hardened Claude Code security config with permission deny rules, shell hooks, and prompt-injection defense in full and lite variants.
- [JeongJaeSoon/agent-guard](https://github.com/JeongJaeSoon/agent-guard) — `PreToolUse` guardrail that blocks an agent from reading `.env` files or writing secret-like values, using gitleaks for detection, with matching Git hook and CI backstops.
- [kenryu42/cc-safety-net](https://github.com/kenryu42/cc-safety-net) — `PreToolUse` guardrail hook blocking destructive git/filesystem commands and secret file access; also supports Codex, Cursor, Gemini CLI, and other agent runtimes.
- [kornysietsma/claude-code-permissions-hook](https://github.com/kornysietsma/claude-code-permissions-hook) — `PreToolUse` hook for more granular, rule-based permission controls than the built-in allow/deny lists.
- [li-zhixin/claude-ignore](https://github.com/li-zhixin/claude-ignore) — `PreToolUse` hook that blocks Claude from reading files matching `.claudeignore` patterns, mirroring `.gitignore` semantics.
- [liberzon/claude-hooks](https://github.com/liberzon/claude-hooks) — `PreToolUse` hook that decomposes compound bash commands and checks each sub-command individually against allow/deny permission patterns.
- [Pantheon-Security/medusa](https://github.com/Pantheon-Security/medusa) — scans `.claude/` hooks, permissions, and skills for compromise before you clone/run a repo; 40,000+ attack-signature patterns.
- [sangrokjung/claude-forge](https://github.com/sangrokjung/claude-forge) — 6-layer security hook stack bundled into a full Claude Code plugin framework.
- [wangbooth/Claude-Code-Guardrails](https://github.com/wangbooth/Claude-Code-Guardrails) — protective hooks preventing accidental code loss via branch protection, automatic checkpointing, and safe commit squashing.

## Notification Hooks

Send a ping to Slack, Telegram, desktop notification center, etc. when Claude needs input or finishes a task.

- [disler/claude-code-hooks-mastery](https://github.com/disler/claude-code-hooks-mastery) — includes `Notification` and `Stop` hook examples with TTS + desktop notification dispatch.
- [shanraisshan/claude-code-hooks](https://github.com/shanraisshan/claude-code-hooks) — adds a distinct voice announcement per hook event so you know what Claude is doing without watching the terminal.

## Observability & Logging Hooks

- [disler/claude-code-hooks-multi-agent-observability](https://github.com/disler/claude-code-hooks-multi-agent-observability) — real-time dashboard for monitoring multiple Claude Code agents via hook event tracking.
- [coleam00/claude-memory-compiler](https://github.com/coleam00/claude-memory-compiler) — hooks capture full sessions, an LLM compiler distills them into a structured, cross-referenced project knowledge base.
- [hansipie/ecotokens](https://github.com/hansipie/ecotokens) — `PreToolUse`/`PostToolUse` hooks filter and compress shell output, file reads, and grep results before they hit the model, with a TUI dashboard tracking token savings per project.

## Git & Commit Hooks

- [parcadei/Continuous-Claude-v3](https://github.com/parcadei/Continuous-Claude-v3) — hooks maintain ledgers/handoffs for context continuity across sessions and commits.
- [blader/taskmaster](https://github.com/blader/taskmaster) — `Stop` hook that keeps the agent working until all plan items and user requests are fully complete, rather than stopping early.

## Formatting / Linting / Testing Gates

- [carlrannaberg/claudekit](https://github.com/carlrannaberg/claudekit) — toolkit of custom hooks/commands including lint/format/test gate hooks.
- [severity1/claude-code-prompt-improver](https://github.com/severity1/claude-code-prompt-improver) — `UserPromptSubmit` hook that rewrites loose prompts into precise ones before Claude sees them.

## Voice / TTS Hooks

- [shanraisshan/claude-code-hooks](https://github.com/shanraisshan/claude-code-hooks) — per-event voice announcements.
- [disler/claude-code-hooks-mastery](https://github.com/disler/claude-code-hooks-mastery) — TTS-on-completion example.

## Session Memory & Context Hooks

- [coleam00/claude-memory-compiler](https://github.com/coleam00/claude-memory-compiler) — auto-captures sessions and compiles a persistent, evolving knowledge base.
- [parcadei/Continuous-Claude-v3](https://github.com/parcadei/Continuous-Claude-v3) — ledger/handoff hooks for context management across long sessions.
- [SethGammon/Citadel](https://github.com/SethGammon/Citadel) — persistent project memory, intent routing, safety hooks, and cost telemetry as one operating layer.

## Frameworks & Toolkits (bundle many hooks)

- [rohitg00/awesome-claude-code-toolkit](https://github.com/rohitg00/awesome-claude-code-toolkit) — 20+ hooks bundled with agents, skills, commands, and rules.
- [davepoon/buildwithclaude](https://github.com/davepoon/buildwithclaude) — hub for finding hooks alongside skills, agents, commands, and marketplace plugins.
- [composio-community/awesome-claude-plugins](https://github.com/composio-community/awesome-claude-plugins) — curated Claude Code plugins that bundle hooks with commands/agents/MCP servers.
- [fcakyon/claude-codex-settings](https://github.com/fcakyon/claude-codex-settings) — battle-tested hook configs across Claude Code, Codex, and Cursor.
- [vibeeval/vibecosystem](https://github.com/vibeeval/vibecosystem) — 73 hooks as part of a larger self-learning multi-agent swarm setup.

## Multi-Agent / Cross-Tool Hooks

Hooks designed to work across Claude Code, Codex, Cursor, Gemini CLI, and other agent runtimes.

- [kenryu42/cc-safety-net](https://github.com/kenryu42/cc-safety-net) — cross-runtime guardrail hook (Claude Code, Codex, Cursor, Gemini CLI, Hermes Agent, and more).
- [first-fluke/oh-my-agent](https://github.com/first-fluke/oh-my-agent) — stop-hook gates and independent judges verifying agent work by artifacts, across multiple agent runtimes.

## Contributing

New hooks, guides, and tools are added regularly — see [CONTRIBUTING.md](CONTRIBUTING.md) for the submission criteria. This list is updated frequently to track newly published hook implementations.

## License

[CC0](LICENSE) — public domain, per [awesome list convention](https://github.com/sindresorhus/awesome/blob/main/awesome.md).
