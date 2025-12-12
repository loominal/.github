# Loominal

**Weaving AI agents together.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue.svg)](https://www.typescriptlang.org/)
[![NATS](https://img.shields.io/badge/NATS-JetStream-green.svg)](https://nats.io/)
[![Status: Beta](https://img.shields.io/badge/Status-Beta-blue.svg)]()

---

Loominal is infrastructure for multi-agent AI systems. Built on [NATS JetStream](https://nats.io/) and the [Model Context Protocol (MCP)](https://modelcontextprotocol.io/), it transforms isolated AI assistants into a coordinated fabric of collaborating agents.

## Components

| Component | Purpose |
|-----------|---------|
| **[Warp](https://github.com/loominal/warp)** | MCP server providing messaging backbone — 16 tools for agent communication |
| **[Weft](https://github.com/loominal/weft)** | Coordinator service for work routing, agent lifecycle, and scaling |
| **[Pattern](https://github.com/loominal/pattern)** | MCP server for persistent agent memory across sessions |
| **[Tools](https://github.com/loominal/tools)** | Docker images and GitHub Actions workflows for CI/CD |

## Quick Start

### 1. Start NATS

```bash
docker run -d --name nats -p 4222:4222 nats:latest -js
```

### 2. Configure Warp

Add to Claude Code MCP config (`~/.claude/mcp.json`):

```json
{
  "mcpServers": {
    "loominal": {
      "command": "docker",
      "args": ["run", "-i", "--rm", "--network=host", "-e", "NATS_URL", "ghcr.io/loominal/warp:latest"],
      "env": {
        "NATS_URL": "nats://localhost:4222"
      }
    }
  }
}
```

### 3. Start Weaving

Your agents can now discover each other, send messages, and coordinate work across machines.

## Key Features

- **Channels** for broadcast messaging with persistent history
- **Agent Registry** for cross-computer agent discovery
- **Direct Messaging** for point-to-point communication
- **Work Queues** with capability-based routing
- **Dynamic Scaling** via SSH, Kubernetes, GitHub Actions

## License

MIT

---

<p align="center">
  <b>Loominal</b> — Weaving AI agents together.
</p>
