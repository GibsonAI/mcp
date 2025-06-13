
[![GibsonAI](./assets/gibsonai-logo.png)](https://gibsonai.com/)

# GibsonAI MCP Server

The GibsonAI MCP Server provides a set of tools to MCP Clients like [Cursor](https://www.cursor.com/), [Windsurf](https://windsurf.com/editor), or [Claude Desktop](https://claude.ai/download). These clients can use these tools to interact with your [GibsonAI](https://app.gibsonai.com/) projects and databases using your natural language instructions.

You can accomplish various tasks with GibsonAI directly in your favorite IDE, for example:

* Create new GibsonAI projects and design database schemas
* View project structure, schema diagrams, a summary of tables and relationships
* Apply schema changes and trigger automatic migrations
* Run SQL queries against your database
* Deploy projects to development or production environments
* Seed tables with mock data
* Build a full-stack apps

Prompt Examples:

- “Create a blogging platform schema with users, posts, and comments.”
- “Add a foreign key from bookings to payments.”
- “Generate mock data for the boooking destination table.”
- “Fetch connection string for my blogging database”
- “Explain how the tables are related in this project.”

## Authentication

You'll need to ensure you're logged in to the [Gibson CLI](https://pypi.org/project/gibson-cli/) before the MCP server will work.

```sh
uvx --from gibson-cli@latest gibson auth login
```

## Connect MCP Clients

- [Cursor](#cursor-setup)
- [Windsurf](#windsurf-setup)
- [Claude Desktop](#claude-desktop-setup)
- [VS Code + GitHub Copilot Setup](#vs-code--github-copilot-setup)


## Cursor Setup <a href="https://dub.sh/gibson-mcp"><img src="https://cursor.com/deeplink/mcp-install-dark.png" alt="Add Gibson MCP server to Cursor" height="32px" align="right" /></a>

Click the `Add to Cursor` button above or go to `Cursor` → `Settings` → `Cursor Settings` → `MCP Tools` and click `New MCP Server`. Update the configuration to include the following:

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

Update the configuration to include the following:

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

Open the `Cascade` chat and, if necessary, refresh the MCP servers

## Claude Desktop Setup

Go to `Claude` → `Settings` → `Developer` and click `Edit Config`

Open the `claude_desktop_config.json` file and update the configuration to include the following:

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

See the [Claude Desktop MCP docs](https://modelcontextprotocol.io/quickstart/user) for more information.

## Claude Code Setup

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

## VS Code + GitHub Copilot Setup

Create or open the `.vscode/mcp.json` file

Update the configuration to include the following:

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

See the official [GitHub Copilot MCP docs](https://docs.github.com/en/copilot/customizing-copilot/extending-copilot-chat-with-mcp#configuring-mcp-servers-in-visual-studio-code) for more information.

## Distribution

Note that this repo is for documentation purposes only. Our MCP server code lives within our [CLI](https://pypi.org/project/gibson-cli/), which allows us to share authentication + API interaction logic with the CLI and have a single distribution. This means we're able to ship new features to you faster.
