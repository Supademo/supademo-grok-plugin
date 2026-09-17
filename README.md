<img src="assets/logo.svg" alt="Supademo" width="64" height="64">

# Supademo plugin

Connect an AI assistant to your Supademo account to find, personalize, edit, and analyze interactive product demos.

This package connects to Supademo's hosted MCP server at `https://mcp.supademo.com/mcp`. Supademo handles authentication, permissions, and tool execution. The package has no local executable, installation script, or API key to configure.

**Status:** Development preview targeting Grok Bot through the Agent Plugins format. OAuth, tool discovery, demo reads, and test-link creation/readback passed in Grok Bot using a custom MCP connection on 2026-09-16. Marketplace listing and installation of this package remain pending. See [validation and release checks](docs/testing.md).

## What you can do

| Workflow | Examples |
| --- | --- |
| Find demos | Search an accessible workspace and inspect a demo's content. |
| Personalize sharing | Create trackable links using variables such as a prospect's name or company. |
| Edit content | Duplicate demos, update copy and hotspots, organize steps, and change appearance. |
| Localize | Translate supported demo content and generate voiceovers when your plan allows it. |
| Analyze engagement | Review demo performance, viewer sessions, and captured lead information. |
| Review Demo Agents | Inspect conversations, summaries, and insights where Demo Agents are enabled. |

Available operations depend on your workspace role, subscription, enabled features, and the tools exposed by the live server. Link variables personalize content where the demo uses those variables; creating a link does not rewrite screenshots or all demo copy.

## Connection

The plugin uses browser-based OAuth. When the client requests authentication, sign in to Supademo and review the authorization screen. Do not paste passwords or access tokens into chat.

The public connection details are:

| Setting | Value |
| --- | --- |
| MCP endpoint | `https://mcp.supademo.com/mcp` |
| Transport | Streamable HTTP |
| Authentication | OAuth 2.0 authorization code with PKCE |
| Setup guide | [Supademo MCP documentation](https://docs.supademo.com/customize/mcp-server) |

During development, ask a Grok Bot to connect the endpoint as a custom remote MCP server, then open **Marketplace → Your plugins → Authenticate**. This tests the hosted connection; this repository does not yet have a verified Grok Bot marketplace installation link. Cursor IDE can load this standard package locally for a separate compatibility check; see [testing](docs/testing.md).

Once a Grok Bot marketplace listing is approved and its installation is verified, customers will be able to add the plugin and complete Supademo authentication from the client. See [release preparation](docs/publishing.md) for the remaining steps.

## Example requests

- "List my Supademo workspaces. Then find onboarding demos in the workspace I choose."
- "Read this demo and suggest clearer hotspot text. Show the suggested changes first."
- "Create a trackable link to this demo for the prospect details I provide, using the demo's existing variables."
- "Review this demo's engagement over the last seven days and explain what the data supports."
- "Summarize the selected Demo Agent conversations and link to the evidence behind each recommendation."

Choose the workspace and demo explicitly when more than one could match. Review proposed edits and publishing actions according to your client's approval controls.

## Access and data

Supademo checks access for each operation. Workspace content operations require an active Creator or Admin membership, and product-specific permissions still apply. The current authorization is tied to your Supademo user; it is not a separate read-only or single-workspace credential.

You can revoke access from Supademo's Connected apps settings. Access tokens currently expire after 90 days, so a client may require authentication again. The plugin does not implement its own token storage or refresh flow.

Data returned by Supademo tools is processed by the AI client you connect. Review that client's data settings, [Supademo's privacy policy](https://supademo.com/privacy-policy), and [Supademo's terms of service](https://supademo.com/terms). Grok Bot plugins are available across bots on the connected account; separate bot profiles are not separate workspace authorization boundaries.

## Package

```text
plugin.json          Plugin identity and metadata
mcp.json             Hosted MCP connection
assets/logo.svg      Supademo brand icon
docs/testing.md      Package and client verification
docs/publishing.md   Marketplace release preparation
LICENSE              License for this package
```

The package follows [Agent Plugins 1.0.0](https://agent-plugins.org/). It contains no bot templates, scheduled routines, or skills. Tool capabilities come from the hosted MCP server.

## Support

- [Supademo MCP documentation](https://docs.supademo.com/customize/mcp-server)
- [Supademo](https://supademo.com)
- Email: support@supademo.com

The package is licensed under MIT. The Supademo name and logo identify the integration and remain Supademo's trademarks.
