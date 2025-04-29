# bonk-mcp MCP server

The bonk-mcp server implements Solana blockchain functionality for the LetsBonk launchpad.

<a href="https://glama.ai/mcp/servers/@bjoernbonk/letsbonk_mcp_server">
  <img width="380" height="200" src="https://glama.ai/mcp/servers/@bjoernbonk/letsbonk_mcp_server/badge" alt="bonk-mcp Server MCP server" />
</a>

## Features
- Token launching: launch any token on letsbonk.fun
- Token trading: buy/sell any token on letsbonk.fun

## Configuration

The bonk-mcp server can be configured in Claude Desktop by adding it to the MCP servers configuration. You'll need to provide:
- Path to the bonk-mcp directory
- Environment variables:
  - `KEYPAIR`: Your Solana keypair
  - `RPC_URL`: Solana RPC endpoint (e.g., https://api.mainnet-beta.solana.com)

## Quickstart

### Install

#### Claude Desktop

On MacOS: `~/Library/Application\ Support/Claude/claude_desktop_config.json`
On Windows: `%APPDATA%/Claude/claude_desktop_config.json`

<details>
  <summary>Development/Unpublished Servers Configuration</summary>
  
  ```json
  "mcpServers": {
    "bonk-mcp": {
      "command": "uv",
      "args": [
        "--directory",
        "<PATH_TO_BONK_MCP_DIRECTORY>/bonk-mcp",
        "run",
        "bonk-mcp"
      ],
      "env": {
        "KEYPAIR": "<YOUR_SOLANA_KEYPAIR>",
        "RPC_URL": "https://api.mainnet-beta.solana.com"
      }
    }
  }
  ```
</details>

<details>
  <summary>Published Servers Configuration</summary>
  
  ```json
  "mcpServers": {
    "bonk-mcp": {
      "command": "uvx",
      "args": [
        "bonk-mcp"
      ],
      "env": {
        "KEYPAIR": "<YOUR_SOLANA_KEYPAIR>",
        "RPC_URL": "https://api.mainnet-beta.solana.com"
      }
    }
  }
  ```
</details>

## Development

### Building and Publishing

To prepare the package for distribution:

1. Sync dependencies and update lockfile:
```bash
uv sync
```

2. Build package distributions:
```bash
uv build
```

This will create source and wheel distributions in the `dist/` directory.

3. Publish to PyPI:
```bash
uv publish
```

Note: You'll need to set PyPI credentials via environment variables or command flags:
- Token: `--token` or `UV_PUBLISH_TOKEN`
- Or username/password: `--username`/`UV_PUBLISH_USERNAME` and `--password`/`UV_PUBLISH_PASSWORD`

### Debugging

Since MCP servers run over stdio, debugging can be challenging. For the best debugging
experience, we strongly recommend using the [MCP Inspector](https://github.com/modelcontextprotocol/inspector).

You can launch the MCP Inspector via [`npm`](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) with this command:

```bash
npx @modelcontextprotocol/inspector uv --directory <PATH_TO_BONK_MCP_DIRECTORY>/bonk-mcp run bonk-mcp
```

Upon launching, the Inspector will display a URL that you can access in your browser to begin debugging.