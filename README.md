# Ollama Code Assistant for Continue

A local-first model configuration for the [Continue](https://www.continue.dev/)
VS Code extension, using [Ollama](https://ollama.com/) to run chat, coding,
autocomplete, embedding, and reranking models locally.

## What this repository provides

The main file is [`config.yaml`](./config.yaml). It assigns a local Ollama
model to each Continue role:

| Continue role | Model | Purpose |
| --- | --- | --- |
| Chat, edit, apply | `qwen2.5-coder:7b` | General coding conversations, code edits, and applying changes |
| Autocomplete | `qwen2.5-coder:1.5b-base` | Fast fill-in-the-middle suggestions while typing |
| Embeddings | `nomic-embed-text:latest` | Converts code and text into vectors for semantic retrieval |
| Reranking | `qllama/bge-reranker-v2-m3:latest` | Reorders retrieved code snippets by relevance |

The primary model advertises the `tool_use` capability for Continue Agent mode.
All model endpoints use Ollama's default local address,
`http://localhost:11434`.

The configuration also enables Continue's codebase, diff, terminal, docs, and
file context providers and includes general-purpose coding rules.

## Requirements

- VS Code with the Continue extension installed.
- Ollama installed and running locally.
- Enough system memory for the models and your editor. Model memory use also
  depends on context size, quantization, and concurrent requests.
- An internet connection for the initial installation of Ollama, Continue, and
  the model files.

This configuration has been used with 16 GB of shared system memory. Actual
speed and memory use vary by hardware and workload; the 7B model may respond
more slowly with long contexts or while other applications are using memory.

## Install

### 1. Install Ollama

Install Ollama for your operating system using the
[official download page](https://ollama.com/download). Start Ollama and confirm
that its local service is available:

```bash
ollama --version
ollama list
```

The local API normally listens at `http://localhost:11434`.

### 2. Download the configured models

Run these commands in a terminal:

```bash
ollama pull qwen2.5-coder:7b
ollama pull qwen2.5-coder:1.5b-base
ollama pull nomic-embed-text:latest
ollama pull qllama/bge-reranker-v2-m3:latest
```

Check that all four are installed:

```bash
ollama list
```

### 3. Install Continue

Install the Continue extension from the
[VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=Continue.continue).
Open Continue once so it creates its configuration directory.

### 4. Install this configuration

Clone this repository into a directory **other than** `~/.continue`; that
directory is also used by Continue for local application data. Back up your
existing configuration before replacing it.

On Linux or macOS, from the cloned repository directory:

```bash
mkdir -p "$HOME/.continue"
if [ -f "$HOME/.continue/config.yaml" ]; then
  cp "$HOME/.continue/config.yaml" "$HOME/.continue/config.yaml.bak"
fi
cp config.yaml "$HOME/.continue/config.yaml"
```

On Windows, from the cloned repository directory, run in PowerShell:

```powershell
$target = Join-Path $HOME ".continue\config.yaml"
New-Item -ItemType Directory -Force (Split-Path $target) | Out-Null
if (Test-Path $target) {
  Copy-Item $target "$target.bak" -Force
}
Copy-Item ".\config.yaml" $target -Force
```

The configuration file location is:

- Linux/macOS: `~/.continue/config.yaml`
- Windows: `%USERPROFILE%\.continue\config.yaml`

In VS Code, run **Continue: Reload Configuration** from the Command Palette
(`Ctrl+Shift+P` on Linux/Windows, `Cmd+Shift+P` on macOS). Select the
Qwen2.5-Coder 7B model in Continue if it is not selected automatically.

## Verify it works

1. In Continue Chat, ask a simple question and confirm that you receive a
   normal text response.
2. In Agent mode, try a small task that requires reading or changing a file.
   Review proposed changes before accepting them.
3. Start typing code in an editor to check autocomplete.
4. Run `ollama ps` after a request to see which model Ollama loaded.

If a model is missing, compare its exact name with `ollama list` and run the
corresponding `ollama pull` command above. If Continue does not show the
configuration, check the Continue output/logs for YAML parsing or model
connection errors and verify that Ollama is running.

## Privacy and security

The configured model endpoint is local (`localhost`), so model requests are
sent to the Ollama service on the same machine. This does not by itself
guarantee that every Continue feature or extension makes no network requests:
for example, documentation retrieval, extension updates, or telemetry may use
network services according to their settings. Review Continue's privacy
settings and the behavior of any enabled context providers.

Do not put API keys, passwords, private project data, or personal tokens in
this repository. Keep Ollama bound to localhost unless you have deliberately
configured and secured remote access. See [SECURITY.md](./SECURITY.md) before
reporting a vulnerability.

## Repository files

- `config.yaml` — Continue configuration and model-role assignments.
- `.gitignore` — excludes Continue-generated runtime data and common local
  secrets.
- `config_schema.json`, `continue_rc_schema.json`, and `types/` — schema and
  type support files present in the configuration directory; they are not
  required when copying only `config.yaml` to another Continue installation.
- `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md`, and `SUPPORT.md` —
  project contribution and community policies.
- `.github/ISSUE_TEMPLATE/` and `.github/PULL_REQUEST_TEMPLATE.md` — GitHub
  issue and pull request forms.

## Updating

To update model files, run the relevant `ollama pull <model>` command again.
To update this configuration, review the repository changes, back up your
local `~/.continue/config.yaml`, and copy the updated file into place. Reload
the Continue configuration afterward.

## Community standards

Please read [CONTRIBUTING.md](./CONTRIBUTING.md) before submitting changes.
This project is released under the [MIT License](./LICENSE).

## References

- [Continue configuration reference](https://docs.continue.dev/reference)
- [Continue model capabilities](https://docs.continue.dev/customize/deep-dives/model-capabilities)
- [Ollama model library](https://ollama.com/library)
- [Ollama API documentation](https://docs.ollama.com/)
