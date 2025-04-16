
[![GibsonAI](https://github.com/user-attachments/assets/26bc1002-f878-4995-a6c5-eb8d5eb69c28)](https://gibsonai.com/)

# Model Context Protocol (MCP)

GibsonAI's MCP server allows tools like [Cursor](https://www.cursor.com/), [Windsurf](https://windsurf.com/editor), or [Claude Desktop](https://claude.ai/download) to create and update projects on your behalf, explain how to interact with the database and hosted APIs, and even write working code for you, all within the comfort of your own IDE. This will greatly improve the context and output of these tools while working with your Gibson project(s).

## Authentication

You'll need to ensure you're logged in to the [Gibson CLI](https://pypi.org/project/gibson-cli/) before the MCP server will work.

```sh
uvx --from gibson-cli@latest gibson auth login
```

## Cursor Setup

Go to `Cursor` → `Settings` → `Cursor Settings` → `MCP` and click `Add new global MCP server`

Update the configuration to add the gibson server:

```json
{
  "mcpServers": {
    "gibson": {
      "command": "uvx",
      "args": ["--from", "gibson-cli@latest", "gibson", "mcp", "run"]
    }
  }
}
```

## Windsurf Setup

Go to `Windsurf` → `Settings` → `Windsurf Settings` → `Cascade` and click `Add server` in the `Model Context Protocol (MCP) Servers` section

In the modal, click `Add custom server`

Update the configuration to add the gibson server:

```json
{
  "mcpServers": {
    "gibson": {
      "command": "uvx",
      "args": ["--from", "gibson-cli@latest", "gibson", "mcp", "run"]
    }
  }
}
```

Open the `Cascade` chat and if necessary, refresh the MCP servers

## Claude Desktop Setup

Go to `Claude` → `Settings` → `Developer` and click `Edit Config`

Open the `claude_desktop_config.json` file and update the configuration to add the gibson server:

```json
{
  "mcpServers": {
    "gibson": {
      "command": "uvx",
      "args": ["--from", "gibson-cli@latest", "gibson", "mcp", "run"]
    }
  }
}
```

## Claude Code

```sh
claude mcp add gibson -- uvx --from gibson-cli@latest gibson mcp run
```

```sh
claude mcp get gibson
```

```txt
gibson:
  Scope: Local (private to you in this project)
  Type: stdio
  Command: uvx
  Args: --from gibson-cli@latest gibson mcp run
  Environment:

To remove this server, run: claude mcp remove "gibson" -s local
```

## VS Code + GitHub Copilot

Create or open the `.vscode/mcp.json` file

```json
{
  "inputs": [],
  "servers": {
    "gibson": {
      "type": "stdio",
      "command": "uvx",
      "args": ["--from", "gibson-cli@latest", "gibson", "mcp", "run"]
    }
  }
}
```

See the [official docs](https://docs.github.com/en/copilot/customizing-copilot/extending-copilot-chat-with-mcp#configuring-mcp-servers-in-visual-studio-code) for more information.

## Distribution

Note that this repo is for documentation purposes only. Our MCP server code lives within our [CLI](https://pypi.org/project/gibson-cli/), which allows us to share authentication + API interaction logic with the CLI and have a single distribution. This means we're able to ship new features to you faster.
