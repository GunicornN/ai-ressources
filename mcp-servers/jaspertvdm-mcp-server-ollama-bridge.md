---
title: "mcp-server-ollama-bridge"
url: "https://github.com/jaspertvdm/mcp-server-ollama-bridge"
description: "🐍 🏠 - Bridge to local Ollama LLM server. Run Llama, Mistral, Qwen and other local models through MCP."
sourceRepo: "jaspertvdm/mcp-server-ollama-bridge"
tags: ["MCP", "IA", "Claude"]
date: 2026-02-13
language: "en"
stars: 1
forks: 1
---

# mcp-server-ollama-bridge

[![PyPI](https://img.shields.io/pypi/v/mcp-server-ollama-bridge)](https://pypi.org/project/mcp-server-ollama-bridge/)

MCP Server - Bridge to local Ollama LLM server.

Part of the [HumoticaOS](https://humotica.com) / [SymbAIon](https://symbaion.eu) ecosystem.

## Installation

```bash
pip install mcp-server-ollama-bridge
```

## Usage

### With Claude Desktop

Add to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "ollama": {
      "command": "mcp-server-ollama-bridge",
      "env": {
        "OLLAMA_HOST": "http://localhost:11434"
      }
    }
  }
}
```

### With Docker

```bash
docker build -t mcp-server-ollama-bridge .
docker run -i -e OLLAMA_HOST=http://host.docker.internal:11434 mcp-server-ollama-bridge
```

## Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `OLLAMA_HOST` | `http://localhost:11434` | Ollama server URL |

## Features

- Connect MCP clients to local Ollama LLM
- Support for all Ollama models
- Streaming responses
- Simple configuration

## Authors

- Jasper van de Meent ([@jaspertvdm](https://github.com/jaspertvdm))
- Root AI (Claude) - root_ai@humotica.nl

## License

MIT

---

**One Love, One fAmIly!**

## Official Distribution

This package is officially distributed via:
- **PyPI**: https://pypi.org/project/mcp-server-ollama-bridge/
- **GitHub**: https://github.com/jaspertvdm/mcp-server-ollama-bridge

> **Note**: Third-party directories may list this package but are not official or verified distribution channels for Humotica software.
