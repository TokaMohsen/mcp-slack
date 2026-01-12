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

To get Slack Bot Token:

1. Create a Slack App:
   - Visit the [Slack Apps page](https://api.slack.com/apps)
   - Click "Create New App"
   - Choose "From scratch"
   - Name your app and select your workspace

2. Configure Bot Token Scopes:
   Navigate to "OAuth & Permissions" and add these scopes:
   - `channels:history` - View messages and other content in public channels
   - `channels:read` - View basic channel information
   - `chat:write` - Send messages as the app
   - `reactions:write` - Add emoji reactions to messages
   - `users:read` - View users and their basic information
   - `users.profile:read` - View detailed profiles about users

4. Install App to Workspace:
   - Click "Install to Workspace" and authorize the app
   - Save the "Bot User OAuth Token" that starts with `xoxb-`

5. Get your Team ID (starts with a `T`) by following [this guidance](https://slack.com/help/articles/221769328-Locate-your-Slack-URL-or-ID#find-your-workspace-or-org-id)


## Environment Variables

- `SLACK_BOT_TOKEN` - Your Slack bot token (required)
- `SLACK_TEAM_ID` - Your Slack team/workspace ID (required)
- `SLACK_CHANNEL_IDS` - Optional comma-separated list of channel IDs to limit access to specific channels


This Slack MCP server is designed to be used with AI assistants through IDE integration.

Tip

For Claude Desktop: Locate and edit the configuration file directly:

Windows: %APPDATA%\Claude\claude_desktop_config.json
macOS: ~/Library/Application Support/Claude/claude_desktop_config.json
Linux: ~/.config/Claude/claude_desktop_config.json
For Cursor: Open Settings → MCP → + Add new global MCP server

## Installation

### Using NPX

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

### Docker

The Docker image is available on Docker Hub at: **[toqafelfel/mcp-slack](https://hub.docker.com/r/toqafelfel/mcp-slack)**

#### Option 1: Pull from Docker Hub (Recommended - No Build Required)

Simply pull the pre-built image:

```bash
docker pull toqafelfel/mcp-slack:latest
```

This is the fastest way to get started! The image is ready to use immediately.

#### Option 2: Build Locally

If you prefer to build the image yourself:

```bash
cd src/slack
docker build -t toqafelfel/mcp-slack .
```

#### Running the Docker Container

Once you have the image (either pulled or built), run it with:

```bash
docker run -i --rm \
  -e SLACK_BOT_TOKEN=xoxb-your-bot-token \
  -e SLACK_TEAM_ID=T01234567 \
  toqafelfel/mcp-slack:latest
```

```json
{
  "mcpServers": {
    "slack": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-e",
        "SLACK_BOT_TOKEN",
        "-e",
        "SLACK_TEAM_ID",
        "-e",
        "SLACK_CHANNEL_IDS",
        "toqafelfel/mcp-slack"
      ],
      "env": {
        "SLACK_BOT_TOKEN": "xoxb-your-bot-token",
        "SLACK_TEAM_ID": "T01234567",
        "SLACK_CHANNEL_IDS": "C01234567, C76543210"
      }
    }
  }
}
```
## License

MIT