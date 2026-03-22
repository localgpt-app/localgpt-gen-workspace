# LocalGPT Workspace

A persistent memory and skills directory for AI agents.

## Documentation

- [World Skills Documentation](https://localgpt.app/docs/gen/world-skills) - Guide to creating 3D world generation skills
- [Proof of Video](https://proofof.video/) - Gallery of prompts and explorable worlds

## Structure

```
├── MEMORY.md          # Long-term curated knowledge
├── HEARTBEAT.md       # Pending tasks for autonomous mode
├── SOUL.md            # AI persona and behavioral guidelines
├── LocalGPT.md        # Standing instructions for conversations
├── memory/            # Daily logs and notes
├── skills/            # Custom skills (world generation, etc.)
├── .mcp.json          # MCP server config for Claude CLI / Codex
├── .gemini/
│   └── settings.json  # MCP server config for Gemini CLI
└── .claude/
    └── settings.local.json  # Claude CLI permissions and MCP settings
```

See [CLAUDE.md](./CLAUDE.md) for detailed documentation on skills format and world.ron structure.

## CLI Backend MCP Configuration

When using LocalGPT Gen interactively with a CLI backend (Claude CLI, Gemini CLI, Codex), these configs tell the CLI to connect to the **existing** Bevy window via MCP relay (`--connect`) instead of spawning a new one.

### `.mcp.json` — Claude CLI / Codex

```json
{
  "mcpServers": {
    "localgpt-gen": {
      "command": "localgpt-gen",
      "args": ["mcp-server", "--connect"]
    }
  }
}
```

### `.gemini/settings.json` — Gemini CLI

```json
{
  "mcpServers": {
    "localgpt-gen": {
      "command": "localgpt-gen",
      "args": ["mcp-server", "--connect"]
    }
  }
}
```

**`--connect`** makes the spawned MCP server process relay tool calls to the running gen process's TCP port (default 9878) instead of creating its own Bevy window. Remove `--connect` if you want standalone MCP mode (each CLI gets its own window).

See [CLI Mode (MCP Relay)](https://localgpt.app/docs/gen/cli-mode) for details.
