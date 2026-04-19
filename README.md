# Hermes Agent

A fork of [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) — an autonomous agent framework powered by Hermes models with tool-calling and structured output support.

> **Personal fork** — I'm using this to experiment with local LLM agents via [Ollama](https://ollama.ai). Main changes: adjusted defaults to work better with local inference.

## Features

- 🤖 Powered by Nous Research's Hermes model family
- 🛠️ Function calling / tool use via structured JSON outputs
- 🔄 Multi-step reasoning and planning
- 🐳 Docker support for easy deployment
- 🔧 Highly configurable via environment variables

## Requirements

- Python 3.10+
- An OpenAI-compatible API endpoint (local or remote)
- Docker (optional)

## Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/your-org/hermes-agent.git
cd hermes-agent
```

### 2. Configure environment

```bash
cp .env.example .env
# Edit .env with your API keys and configuration
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the agent

```bash
python main.py
```

## Docker

```bash
docker build -t hermes-agent .
docker run --env-file .env hermes-agent
```

## Configuration

See [`.env.example`](.env.example) for all available configuration options.

Key settings:

| Variable | Description | Default |
|---|---|---|
| `OPENAI_API_BASE` | API base URL | `http://localhost:11434/v1` |
| `OPENAI_API_KEY` | API key | `sk-...` |
| `MODEL_NAME` | Model to use | `NousResearch/Hermes-3-Llama-3.1-8B` |
| `MAX_ITERATIONS` | Max agent loop iterations | `5` |
| `TEMPERATURE` | Sampling temperature | `0.1` |
| `REQUEST_TIMEOUT` | HTTP request timeout in seconds | `120` |

> **Note:** I lowered `MAX_ITERATIONS` from `10` to `5` — found that most tasks complete well within 5 steps locally, and it prevents runaway loops when the model gets confused.

> **Note:** I lowered `TEMPERATURE` from `0.3` to `0.1` — at 0.3 the model occasionally went off-script with tool arguments; 0.1 keeps outputs more deterministic and reliable for tool-calling.

> **Note:** Added `REQUEST_TIMEOUT` defaulting to `120` seconds — Ollama on my machine can be slow to respond on first inference (model loading), and the original 30s default caused frequent timeout errors on cold starts.

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feat/my-feature`)
3. Commit your changes
4. Open a Pull Request

Please use the issue templates for bug reports and feature requests.

## License

MIT License — see [LICENSE](LICENSE) for details.
