# Slack MCP Server

MCP server for interacting with Slack workspace using the Slack Web API.

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

## Building

```bash
npm install
npm run build
```

## Docker

Build the Docker image:

```bash
docker build -t slack-mcp -f src/slack/Dockerfile .
```

Run the container:

```bash
docker run -e SLACK_BOT_TOKEN=your_token -e SLACK_TEAM_ID=your_team_id slack-mcp
```

## License

MIT