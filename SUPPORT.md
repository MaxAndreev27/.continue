# Support

## Before asking for help

1. Check the setup and troubleshooting sections in the
   [README](./README.md).
2. Confirm Ollama is running with `ollama list`.
3. Confirm the model tag in `config.yaml` exactly matches a tag shown by
   `ollama list`.
4. Run **Continue: Reload Configuration** in VS Code.
5. Check the Continue output/logs for configuration or connection errors.

## Asking a question

Use a GitHub issue for reproducible configuration problems, or a GitHub
Discussion if Discussions are enabled for the repository. Include:

- Operating system and Continue version.
- Ollama version (`ollama --version`).
- Relevant model tags and the Continue role being tested.
- The steps to reproduce and the expected and actual behavior.

Do not attach API keys, private prompts, full session exports, logs containing
source code, or other sensitive information. Redact local usernames and
machine-specific paths where practical.

For suspected security vulnerabilities, follow [SECURITY.md](./SECURITY.md)
instead of opening a public issue.
