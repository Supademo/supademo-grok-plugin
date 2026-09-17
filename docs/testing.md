# Plugin verification

The checks below distinguish package validity from authenticated client compatibility. Passing a JSON schema or HTTP discovery check does not prove Grok Bot can authorize and execute tools.

## Package checks

Validate `plugin.json` and `mcp.json` against their declared Agent Plugins 1.0.0 JSON schemas:

- https://agent-plugins.org/schemas/1.0.0/plugin.schema.json
- https://agent-plugins.org/schemas/1.0.0/mcp.schema.json

Also verify:

- The configured server is `https://mcp.supademo.com/mcp` with type `streamable-http`.
- The package contains no credentials, environment values, customer information, local executables, or installation hooks.
- All relative links and referenced assets resolve.
- The SVG logo is the public Supademo icon and contains no scripts or external resources.
- `git diff --check` passes.

## Public discovery

Fetch these endpoints without credentials:

```sh
curl --fail --silent --show-error https://mcp.supademo.com/.well-known/oauth-protected-resource
curl --fail --silent --show-error https://app.supademo.com/.well-known/oauth-authorization-server
```

Confirm the protected resource identifies `https://mcp.supademo.com/mcp`, and that authorization metadata advertises authorization-code flow, S256 PKCE, and registration/authorization/token endpoints.

An unauthenticated MCP request should be rejected with an authentication challenge. Do not store access tokens, authorization codes, cookies, or customer responses in this repository.

## Cursor IDE development check

The [Cursor local plugin testing guide](https://cursor.com/docs/plugins#test-plugins-locally) documents local development under `~/.cursor/plugins/local/<name>`. Copy this package into a new directory there and reload Cursor. Use a real copy; external symlinks can be skipped. Do not overwrite an existing installed plugin without reviewing it.

This checks the package in Cursor IDE only. It does not establish Grok Bot compatibility, because Grok Bot performs remote connections from its cloud infrastructure.

## Grok Bot acceptance

Use a test Supademo account/workspace with synthetic demo and lead data. Use the current Grok Bot custom-connection or development-plugin UI if available; otherwise arrange a private test listing with the marketplace team. The published marketplace installation instructions do not establish a local-folder installation method for Grok Bot.

Record the Grok Bot version, date, test workspace, result, and any redacted error for each check. Keep account IDs and private evidence outside this public package.

| Check | Expected result |
| --- | --- |
| OAuth sign-in | Browser authorization completes and the connection becomes available. |
| Tool discovery | Supademo tools are discoverable in Grok Bot. |
| List workspaces | Returns workspaces allowed by the connected account. |
| Read test demo | Returns the selected synthetic demo without changing it. |
| Create test link | Creates exactly one trackable link with the requested variables, where entitled. |
| Inspect result | The returned link opens and its variables match supported demo content. |
| Reconnect/revoke | Revoking the connection prevents further authenticated use; reconnecting works. |
| Workspace access | Operations reject a workspace the test account cannot access. |
| Product gates | Missing entitlements produce an actionable error rather than bypassing the gate. |
| Repeated prompt | The bot checks prior work and does not accidentally create duplicate links. |

Use a disposable account for revocation testing so existing production connections are not disrupted. Standard write tools are not guaranteed idempotent; an uncertain write outcome must be checked before retrying. Client approval controls are separate from Supademo's server-side authorization.

## Release status

- Package schema validation: passed against both canonical Agent Plugins 1.0.0 schemas on 2026-09-16. Relative documentation links and the static SVG asset also passed inspection.
- Public discovery: both metadata endpoints returned HTTP 200 on 2026-09-16. The resource, OAuth endpoints, S256 PKCE, and public-client registration metadata match the configuration. An unauthenticated MCP initialize request returned HTTP 401 with the expected Bearer resource-metadata challenge.
- Cursor IDE authenticated workflow: pending.
- Grok Bot authenticated workflow: pending; the local app is at first-run onboarding, before connection setup.
- Public marketplace listing: pending.

Update these statuses only from observed results. A public source repository is not a marketplace listing.
