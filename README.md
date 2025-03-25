# @kazuph/mcp-devin MCP Server with Slack Integration

MCP server for Devin AI with Slack integration

<a href="https://glama.ai/mcp/servers/@kazuph/mcp-devin">
  <img width="380" height="200" src="https://glama.ai/mcp/servers/@kazuph/mcp-devin/badge" alt="MCP-Devin MCP server" />
</a>

This is a TypeScript-based MCP server that provides integration between Devin AI and Slack. The server enables:

- Creating Devin sessions and automatically posting tasks to Slack
- Sending messages to Devin sessions and the corresponding Slack threads
- Managing sessions with enhanced Slack integration

## Features

### Slack Integration
- Automatically posts Devin tasks to Slack with `@Devin` mentions
- Maintains thread context between Devin sessions and Slack threads
- Uses Slack Bot token for authentication

### Tools
- `create_devin_session` - Create a new Devin session and post to Slack
  - Posts task to a designated Slack channel with `@Devin` mention
  - Returns session details and Slack message information
- `send_message_to_session` - Send a message to a Devin session with optional Slack thread
  - Can simultaneously post to the Slack thread when provided
- `get_devin_session` - Get session details with optional Slack message history
- `list_devin_sessions` - List all Devin sessions
- `get_organization_info` - Get information about your Devin organization

## Development

Install dependencies:
```bash
pnpm install
```

Build the server:
```bash
pnpm run build
```

For development with auto-rebuild:
```bash
pnpm run watch
```

## Configuration

### MCP Server Configuration

The server is configured through the MCP server configuration file. Add the following to your configuration:

```json
"devin-mono": {
  "command": "node",
  "args": ["/path/to/mcp-devin/build/index.js"],
  "env": {
    "DEVIN_API_KEY": "your-devin-api-key",
    "DEVIN_ORG_NAME": "Your Organization",
    "SLACK_BOT_TOKEN": "xoxb-your-slack-bot-token",
    "SLACK_DEFAULT_CHANNEL": "general"
  }
}
```

### Required Environment Variables

The following environment variables must be set in the `env` section:

- `DEVIN_API_KEY`: Your Devin API key
- `DEVIN_ORG_NAME`: (Optional) Your organization name, defaults to "Default Organization"
- `DEVIN_BASE_URL`: (Optional) Base URL for the Devin API, defaults to "https://api.devin.ai/v1"
- `SLACK_BOT_TOKEN`: Your Slack Bot User OAuth Token (starts with xoxb-)
- `SLACK_DEFAULT_CHANNEL`: The default Slack channel where messages will be posted. You can use either:
  - Channel ID (e.g. `C123ABC456`)
  - Channel name (e.g. `general` or `#general`)

## Installation

To use with Claude Desktop, add the server config:

On MacOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
On Windows: `%APPDATA%/Claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "@kazuph/mcp-devin": {
      "command": "/path/to/@kazuph/mcp-devin/build/index.js"
    }
  }
}
```

### Debugging

Since MCP servers communicate over stdio, debugging can be challenging. We recommend using the [MCP Inspector](https://github.com/modelcontextprotocol/inspector), which is available as a package script:

```bash
pnpm run inspector
```

The Inspector will provide a URL to access debugging tools in your browser.