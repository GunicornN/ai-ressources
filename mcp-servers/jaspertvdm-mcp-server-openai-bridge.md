---
title: "mcp-server-openai-bridge"
url: "https://github.com/jaspertvdm/mcp-server-openai-bridge"
description: "🐍 ☁️ - Bridge to OpenAI API. Access GPT-4, GPT-4o and other OpenAI models through MCP."
sourceRepo: "jaspertvdm/mcp-server-openai-bridge"
tags: ["MCP", "IA", "Claude", "OpenAI"]
date: 2026-02-13
language: "en"
stars: 1
forks: 1
---

# mcp-server-openai-bridge

[![PyPI](https://img.shields.io/pypi/v/mcp-server-openai-bridge)](https://pypi.org/project/mcp-server-openai-bridge/)

MCP Server - Bridge to OpenAI API.

Part of the [HumoticaOS](https://humotica.com) / [SymbAIon](https://symbaion.eu) ecosystem.

## Installation

```bash
pip install mcp-server-openai-bridge
```

## Usage

### With Claude Desktop

Add to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "openai": {
      "command": "mcp-server-openai-bridge",
      "env": {
        "OPENAI_API_KEY": "sk-..."
      }
    }
  }
}
```

### With Docker

```bash
docker build -t mcp-server-openai-bridge .
docker run -i -e OPENAI_API_KEY=sk-... mcp-server-openai-bridge
```

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `OPENAI_API_KEY` | Yes | Your OpenAI API key |

## Features

- Connect MCP clients to OpenAI API
- Support for GPT-4, GPT-3.5, and other models
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
- **PyPI**: https://pypi.org/project/mcp-server-openai-bridge/
- **GitHub**: https://github.com/jaspertvdm/mcp-server-openai-bridge

> **Note**: Third-party directories may list this package but are not official or verified distribution channels for Humotica software.
