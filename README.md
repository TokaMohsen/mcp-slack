# Slack MCP Server

MCP server for interacting with Slack workspace using the Slack Web API.

> **Disclaimer:** This project is not affiliated with, endorsed by, or sponsored by Slack Technologies, Inc. "Slack" is a registered trademark of Slack Technologies, Inc. This is an independent integration built using Slack's public APIs.

## Features

This Slack MCP server provides the following tools:

- `slack_list_channels` - List public or pre-defined channels in the workspace
- `slack_post_message` - Post a new message to a Slack channel
- `slack_reply_to_thread` - Reply to a specific message thread
- `slack_delete_message` - Delete a specific message
- `slack_add_reaction` - Add a reaction emoji to a message
- `slack_get_channel_history` - Get recent messages from a channel
- `slack_get_thread_replies` - Get all replies in a message thread
- `slack_get_users` - Get a list of all users in the workspace
- `slack_get_user_profile` - Get detailed profile information for a specific user

## Requirements

- Node.js 22+
- Slack Bot Token with appropriate scopes
- Slack Team ID

## Environment Variables

- `SLACK_BOT_TOKEN` - Your Slack bot token (required)
- `SLACK_TEAM_ID` - Your Slack team/workspace ID (required)
- `SLACK_CHANNEL_IDS` - Optional comma-separated list of channel IDs to limit access to specific channels

## Installation

### Using NPX (Recommended)

No installation needed! Just configure Claude Desktop or VS Code to use:

```bash
npx -y @tokamohsen/mcp-slack
```

### From Source

```bash
git clone https://github.com/tokamohsen/mcp-slack.git
cd mcp-slack/src/slack
npm install
npm run build
```

## Usage Examples

### Quick Start with Claude Desktop

Add to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "slack": {
      "command": "npx",
      "args": ["-y", "@tokamohsen/mcp-slack"],
      "env": {
        "SLACK_BOT_TOKEN": "xoxb-your-bot-token",
        "SLACK_TEAM_ID": "T01234567"
      }
    }
  }
}
```

### Docker

Build the Docker image:

```bash
docker build -t tokamohsen/mcp-slack -f src/slack/Dockerfile .
```

Run the container:

```bash
docker run -e SLACK_BOT_TOKEN=your_token -e SLACK_TEAM_ID=your_team_id tokamohsen/mcp-slack
```

## License

MIT