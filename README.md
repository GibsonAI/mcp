[![GibsonAI](https://github.com/user-attachments/assets/a083db7e-96df-4c0c-8747-3c0e11307ab4)](https://gibsonai.com/)

# GibsonAI MCP Server

The GibsonAI Model Context Protocol Server provides a set of tools to MCP Clients like [Cursor](https://www.cursor.com/), [Windsurf](https://windsurf.com/editor), or [Claude Desktop](https://claude.ai/download). These clients can use these tools to interact with your [GibsonAI](https://app.gibsonai.com/) projects and databases using your natural language instructions.

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

## Usage Examples

- [Convert Images, PDF, Excel sheets, or JSON to a relational database](https://docs.gibsonai.com/guides/create-database-from-any-er-diagram-image)
- [Automatic PR creation on GitHub for database schema change](https://docs.gibsonai.com/guides/automatic-pr-creation-for-database-schema-change)

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
- [Cline (VS Code Extension)](#cline-vs-code-extension-setup)


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

## Cline (VS Code Extension) Setup

1. Open **Cline** in VS Code:  
   Go to **Sidebar → Cline icon**.

2. To configure MCP Servers in Cline, you need to modify the `cline_mcp_settings.json` file. Click the **MCP Servers** icon → go to **Installed** → click **Configure MCP Servers** to open the configuration file.

3. Add the following `gibson` server entry inside the `mcpServers` object:

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

4. Save the file. Cline should reload the configuration automatically.

## 🔧 Supported Tools

### 🗂 `get_projects`
**Title:** List all existing projects  
**Description:** Retrieves all GibsonAI projects associated with the authenticated user. Useful when the user refers to a project by name but you need the UUID. If a `.gibsonai` file exists, use it instead unless the user intends otherwise.

### 🆕 `create_project`
**Title:** Create a new project  
**Description:** Creates a new GibsonAI project. Check for an existing `.gibsonai` file or similar project names before creation. Prompt the user to update or create the `.gibsonai` file with the new UUID.


### 🔍 `get_project_details`
**Title:** Fetch project metadata  
**Description:** Returns metadata and configuration for a given project using its UUID. Ideal when working with an existing `.gibsonai` file to load project-specific context.

### 🔗 `get_project_hosted_database_details`
**Title:** Get hosted database connection details  
**Description:** Returns credentials, connection string, dialect, and other necessary details for querying the hosted GibsonAI database. Useful for building queries or integrating with tools.

### ✏️ `update_project`
**Title:** Rename a project  
**Description:** Updates the project name using its UUID. Currently, only the `project_name` field is supported.


### 🧠 `submit_data_modeling_request`
**Title:** Submit schema modeling request  
**Description:** Submit any natural-language data modeling request (e.g., create, modify schema). This tool fully handles the request using GibsonAI's internal modeler and should be used instead of any manual schema design.


### 🚀 `deploy_project`
**Title:** Deploy to database(s)  
**Description:** Triggers automatic schema migrations and deploys the current schema to all GibsonAI supported databases.


### 📐 `get_project_schema`
**Title:** Get working schema  
**Description:** Retrieves the current state of the schema including unpublished or un-deployed changes.

### ✅ `get_deployed_schema`
**Title:** Get live schema  
**Description:** Fetches the schema currently deployed to the primary hosted database. Use this to compare against the working schema or confirm deployment to your primary database (e.g. Production)

### 🧾 `query_database`
**Title:** Run SQL queries  
**Description:** Runs the provided SQL query against a database by using the API key associated with that database. Ensure correct quoting for identifiers depending on the SQL dialect (e.g., backticks for MySQL, double quotes for PostgreSQL).


## Distribution

Note that this repo is for documentation purposes only. Our MCP server code lives within our [CLI](https://pypi.org/project/gibson-cli/), which allows us to share authentication + API interaction logic with the CLI and have a single distribution. This means we're able to ship new features to you faster.
