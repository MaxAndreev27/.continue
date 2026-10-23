# Contributing

Thank you for considering a contribution to Ollama Code Assistant for
Continue. Contributions should keep the configuration useful, understandable,
and safe to publish.

## Before you start

- Check existing issues and pull requests for related work.
- For a substantial change, open an issue first to discuss the approach.
- Keep changes focused on this Continue/Ollama configuration.
- Do not include credentials, private prompts, project source code, local
  databases, logs, or session exports.

## Making a change

1. Fork the repository and create a branch for your change.
2. Edit the relevant configuration or documentation.
3. Keep model identifiers and Ollama pull commands consistent with the
   configured roles.
4. Update the README when setup requirements, model assignments, or behavior
   changes.
5. Submit a pull request with a clear summary and rationale.

## Validation checklist

Before opening a pull request:

- Parse `config.yaml` with a YAML 1.2-compatible parser.
- Confirm every configured model can be pulled from Ollama and that the
  documented tags match the configuration.
- Check that model roles and capabilities are intentional. In particular,
  `tool_use` should only be set for a model that supports tool calling.
- Run `git diff --check`.
- Review the full diff for secrets, personal information, machine-specific
  paths, and generated runtime files.

No test suite or build step is currently required for this configuration-only
repository.

## Pull requests

Explain the problem, the change, and how you validated it. If model behavior
was tested, include the Ollama version, model tag, and a brief reproducible
description. Do not include private prompts or sensitive code in the report.

By submitting a contribution, you agree that it is provided under the
repository's MIT License.
