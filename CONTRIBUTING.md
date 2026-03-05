# Contributing to Rusty GitClaw

Thanks for your interest in contributing to Rusty GitClaw! Here's how to get started.

## Getting Started

1. Fork the repository
2. Clone your fork:
   ```bash
   git clone https://github.com/<your-username>/rusty-gitclaw.git
   cd rusty-gitclaw
   ```
3. Build the project:
   ```bash
   cargo build --workspace
   ```
4. Run tests:
   ```bash
   cargo test --workspace
   ```
5. Run clippy:
   ```bash
   cargo clippy --workspace
   ```

## Development Workflow

1. Create a feature branch from `main`:
   ```bash
   git checkout -b feat/my-feature
   ```
2. Make your changes
3. Run `cargo build --workspace` to verify compilation
4. Run `cargo test --workspace` to ensure tests pass
5. Run `cargo clippy --workspace` for lint checks
6. Commit your changes with a clear message
7. Push and open a pull request

## Project Structure

```
rusty-gitclaw/
├── pi-ai/                  # LLM provider abstraction
│   └── src/
│       ├── types.rs        # Core types (Message, Content, Model, Usage)
│       ├── models.rs       # Model registry (383 models, 8 providers)
│       ├── stream.rs       # Streaming dispatcher
│       ├── providers/      # Anthropic, OpenAI, Google providers
│       └── ...
├── pi-agent-core/          # Agent loop engine
│   └── src/
│       ├── types.rs        # AgentTool trait, AgentEvent enum
│       ├── agent_loop.rs   # Core stream → tool → loop cycle
│       ├── agent.rs        # Agent struct with prompt/subscribe/abort
│       └── ...
└── gitclaw/                # CLI + SDK + tools + voice
    └── src/
        ├── main.rs         # CLI with clap + REPL with rustyline
        ├── sdk.rs          # query() function
        ├── loader.rs       # Agent manifest loading
        ├── tools/          # Built-in tools (cli, read, write, memory)
        ├── voice/          # OpenAI Realtime WebSocket adapter
        └── ...
```

## Guidelines

- **Rust stable** — target the latest stable Rust toolchain
- **No unsafe** — avoid `unsafe` unless absolutely necessary and well-documented
- **Keep it simple** — avoid over-engineering; match the TypeScript version's behavior
- **Test your changes** — add unit tests for new functionality
- **One concern per PR** — keep pull requests focused and reviewable
- **Clippy clean** — `cargo clippy --workspace` should pass without warnings for new code

## Commit Messages

Use clear, descriptive commit messages:

- `Add streaming support for Mistral provider`
- `Fix memory tool path resolution on Windows`
- `Update agent loop to respect max_turns constraint`

## Architecture Notes

This is a **pure translation** of the [TypeScript GitClaw](https://github.com/open-gitagent/gitclaw). When in doubt about behavior, refer to the TypeScript implementation. Key translation patterns:

| TypeScript | Rust |
|---|---|
| `AsyncGenerator<T>` | `mpsc::UnboundedReceiver<T>` |
| `EventStream` (push/end) | `mpsc::unbounded_channel` + `oneshot` |
| `AbortSignal` | `CancellationToken` (tokio-util) |
| `interface AgentTool` | `#[async_trait] trait AgentTool` |
| `child_process.spawn` | `tokio::process::Command` |
| `fs/promises` | `tokio::fs` |

## Adding a New Provider

1. Create `pi-ai/src/providers/your_provider.rs`
2. Implement the `ApiProvider` trait
3. Register it in `pi-ai/src/providers/mod.rs`
4. Add models to `pi-ai/data/models.json`
5. Add the API key mapping in `pi-ai/src/env_api_keys.rs`

## Reporting Issues

- Search existing issues before opening a new one
- Include reproduction steps, expected vs actual behavior
- Include your Rust version (`rustc --version`) and OS

## Code of Conduct

Be respectful and constructive. We're all here to build something useful together.

## License

By contributing, you agree that your contributions will be licensed under the [MIT License](./LICENSE).
