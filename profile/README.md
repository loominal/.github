# Loominal

**Weaving AI agents together.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue.svg)](https://www.typescriptlang.org/)
[![NATS](https://img.shields.io/badge/NATS-JetStream-green.svg)](https://nats.io/)
[![Status: Beta](https://img.shields.io/badge/Status-Beta-blue.svg)]()

---

Loominal is infrastructure for multi-agent AI systems. Built on [NATS JetStream](https://nats.io/) and the [Model Context Protocol (MCP)](https://modelcontextprotocol.io/), it transforms isolated AI assistants into a coordinated fabric of collaborating agents.

## The Problem

Today's AI coding assistants are **islands**. Each Claude Code session, each GitHub Copilot instance operates in complete isolation. There's no way for them to:

- Share context or findings with other agents
- Hand off work based on capabilities or access rights
- Coordinate on complex, multi-part tasks
- Scale up or down based on workload

**Loominal weaves them together.**

## The Fabric

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              WARP (Backbone)                                │
│                    NATS JetStream + MCP Server                              │
│              Persistent messaging infrastructure for agents                 │
└─────────────────────────────────────────────────────────────────────────────┘
        ▲               ▲               ▲               ▲               ▲
        │               │               │               │               │
   ┌────┴────┐     ┌────┴────┐     ┌────┴────┐     ┌────┴────┐     ┌────┴────┐
   │ Claude  │     │ Claude  │     │ Copilot │     │  WEFT   │     │  Your   │
   │  Code   │     │  Code   │     │   CLI   │     │ Service │     │  Agent  │
   │ (Home)  │     │ (Cloud) │     │ (Work)  │     │         │     │         │
   └─────────┘     └─────────┘     └─────────┘     └─────────┘     └─────────┘
     Agent           Agent           Agent        Coordinator        Agent
```

## Repositories

| Repository | Description |
|------------|-------------|
| **[warp](https://github.com/loominal/warp)** | MCP server providing 16 tools for agent communication — messaging backbone |
| **[weft](https://github.com/loominal/weft)** | Work coordinator with intelligent routing and dynamic agent spin-up |
| **[pattern](https://github.com/loominal/pattern)** | MCP server for persistent agent memory across sessions |
| **[tools](https://github.com/loominal/tools)** | Docker images and GitHub Actions workflows for CI/CD integration |
| **[loominal](https://github.com/loominal/loominal)** | Project overview and documentation |

## Quick Start

### 1. Start NATS

```bash
docker run -d --name nats -p 4222:4222 nats:latest -js
```

### 2. Install Warp

```bash
npm install -g @loominal/warp
```

Configure Claude Code (`~/.claude/mcp.json`):

```json
{
  "mcpServers": {
    "loominal": {
      "command": "warp",
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

## Status

**Beta Release** — All core features implemented and tested. Ready for early adopters.

## License

MIT License

---

<p align="center">
  <b>Loominal</b> — Weaving AI agents together.
</p>
