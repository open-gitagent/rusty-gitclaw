# Security Policy

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| 0.1.x   | :white_check_mark: |

## Reporting a Vulnerability

If you discover a security vulnerability in Rusty GitClaw, please report it responsibly:

1. **Do not** open a public GitHub issue for security vulnerabilities
2. Email the maintainers or use [GitHub's private vulnerability reporting](https://github.com/open-gitagent/rusty-gitclaw/security/advisories/new)
3. Include a description of the vulnerability, steps to reproduce, and potential impact
4. We will acknowledge receipt within 48 hours and provide a timeline for a fix

## Security Considerations

Rusty GitClaw executes shell commands and reads/writes files on behalf of the AI agent. Users should be aware that:

- The `cli` tool executes arbitrary shell commands in the agent directory
- The `read` and `write` tools can access files within the agent directory
- Hook scripts are executed with the same permissions as the gitclaw process
- API keys are read from environment variables and should never be committed to git

## Best Practices

- Run gitclaw in a sandboxed environment when working with untrusted repositories
- Use the `allowedTools` / `disallowedTools` options to restrict tool access
- Use hooks (`pre_tool_use`) to gate dangerous operations
- Never commit API keys or tokens to your agent repository
- Review declarative tool scripts before enabling them
