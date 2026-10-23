# Security Policy

## Supported versions

Security fixes are intended for the current version on the `main` branch.
There are no separately maintained release branches at this time.

## Reporting a vulnerability

Please report suspected vulnerabilities privately using GitHub's
**Report a vulnerability** option in the repository's Security tab, if
private vulnerability reporting is enabled. Do not publish credentials,
exploitable details, or private user data in a public issue or pull request.

If private vulnerability reporting is unavailable, contact the maintainers
through a private channel listed on their GitHub profile and first send only a
brief, non-sensitive description to arrange secure coordination.

Include the affected file or feature, the impact, and safe reproduction
details. Allow maintainers reasonable time to investigate and prepare a fix
before public disclosure.

## Configuration-specific guidance

- Never commit API keys, access tokens, passwords, private keys, or `.env`
  files.
- Treat Continue sessions, logs, prompts, and local databases as potentially
  sensitive; they may contain user code or conversation content.
- Keep Ollama's API bound to localhost unless remote access is intentionally
  configured and appropriately secured.
- Review changes to model providers, endpoints, and context providers for
  unintended external data transmission.
- If a credential is exposed, revoke or rotate it immediately. Removing it
  from the latest file does not remove it from Git history.
