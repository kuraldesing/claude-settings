# claude-settings

My personal Claude setup with battle-tested commands and MCP servers that I use daily.

## MCP Servers

The MCP (Model Context Protocol) configuration lives in [`.mcp.json`](./.mcp.json). These are some solid MCP server repos worth checking out:

- [Slack MCP Server](https://github.com/ubie-oss/slack-mcp-server) - Connect Claude to Slack workspaces
- [GitHub MCP Server](https://github.com/github/github-mcp-server) - GitHub integration for Claude
- [Context7](https://github.com/upstash/context7) - Upstash's context management server
- [Azure MCP](https://github.com/Azure/azure-mcp) - Azure services integration

## Commands

Custom Claude commands that make life easier, stored in [`.claude/commands/`](./.claude/commands/):

- [`commit.md`](./.claude/commands/commit.md) - Automated commit creation with conventional commit messages