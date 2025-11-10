# MCP Demo Content

This repository manages the content and prompts for MCP (Model Context Protocol) demo storage connections.

## Overview

This repo serves three primary purposes:

1. **Demo Prompts**: Manages the prompt configurations used in demo storage connections
2. **S3 Demo Content**: Maintains the actual demo files and datasets displayed in the demo buckets
3. **MCP Servers**: Curates a list of third-party MCP servers with their connection details and logos

## Repository Structure

```
.
├── prompts/
│   └── prompts.json          # Prompt configurations for demo storage connections
├── s3-files/                 # Demo content synced to S3 buckets
└── mcp-servers/
    ├── logos/                # Logos for third-party MCP servers
    └── servers.json          # List of third-party MCP servers with connection details
```

## Automated S3 Sync

Changes to the `s3-files/` directory are automatically synchronized to S3 buckets when pushed to the `main` branch.

### How It Works

- **Trigger**: Any push to `main` that modifies files in `s3-files/`
- **Action**: GitHub Actions workflow (`.github/workflows/sync-s3.yml`) runs automatically
- **Sync**: Files are synced to both staging and production S3 buckets
- **Deletion**: Files removed from the repo are also deleted from S3 (`--delete` flag)

### Target Buckets

- **Staging**: `vendia-demo-staging`
- **Production**: `vendia-demo-share`

## Making Changes

### Updating Demo Content

1. Add, modify, or delete files in the `s3-files/` directory
2. Commit your changes
3. Push to `main` branch
4. The GitHub Action will automatically sync changes to both S3 buckets

### Updating Prompts

1. Edit `prompts/prompts.json`
2. Commit and push to `main`
3. The UI fetches the raw json file, after a push to main you should see the prompt changes show up right away

### Managing MCP Servers

The `mcp-servers/servers.json` file contains a curated list of third-party MCP servers available for integration.

**To add a new server:**

1. Add the server's logo to `mcp-servers/logos/`
2. Add a new entry to `mcp-servers/servers.json` with:
   - `name`: Server name
   - `description`: Brief description of the service
   - `mcpUrl`: The MCP endpoint URL
   - `logoUrl`: Raw GitHub URL to the logo file
3. Commit and push to `main`
4. The UI fetches the raw json file, after a push to main you should see the new server show up right away
