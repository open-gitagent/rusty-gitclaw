# Changelog

All notable changes to this project will be documented in this file.

## [0.1.0] - 2025-03-04

### Added

- Initial Rust port of [GitClaw](https://github.com/open-gitagent/gitclaw)
- **pi-ai crate**: LLM provider abstraction with streaming support
  - Anthropic Messages API (Claude)
  - OpenAI Chat Completions (GPT-4o, o1, o3)
  - Google Generative AI (Gemini)
  - Built-in registry of 383 models across 8 providers
  - SSE streaming with event mapping
  - JSON Schema validation for tool arguments
- **pi-agent-core crate**: Agent loop engine
  - Stream response -> execute tool calls -> loop pattern
  - Broadcast event system for subscribers
  - CancellationToken-based abort support
- **gitclaw crate**: Full CLI + SDK
  - Interactive REPL with rustyline
  - Single-shot mode (`--prompt`)
  - Local repo mode (`--repo` with auto clone/branch/push)
  - Voice mode (`--voice`) with OpenAI Realtime WebSocket
  - Built-in tools: cli, read, write, memory
  - Declarative YAML tool definitions
  - Skills, workflows, knowledge, examples discovery
  - Script-based lifecycle hooks
  - Compliance validation and JSONL audit logging
  - Environment config with YAML deep merge
  - Agent inheritance and scaffolding
- Single 12MB static binary with zero runtime dependencies
- Full compatibility with TypeScript GitClaw agent repos
