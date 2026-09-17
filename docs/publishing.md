# Marketplace release preparation

The package targets Grok Bot using the portable Agent Plugins format. The documented submission route reviewed is the Cursor marketplace, where Quo also has a listing. Confirm that an accepted submission will be available in Grok Bot; Cursor IDE availability alone is not that confirmation.

## Listing draft

| Field | Draft |
| --- | --- |
| Name | Supademo |
| Description | Find, personalize, and analyze interactive product demos. Connect Supademo to work with demos, trackable links, and Demo Agent conversations. |
| Repository | https://github.com/Supademo/supademo-grok-plugin |
| Documentation | https://docs.supademo.com/customize/mcp-server |
| Website | https://supademo.com |
| Support | support@supademo.com |
| Logo | `assets/logo.svg` |

The core Agent Plugins manifest does not allow a top-level `logo` field. The live publisher application has a **Logotype URL** field requesting a square SVG or PNG with a background plate. The public Supademo icon is available at `https://cdn.supademo.com/supademo_logo_icon.svg` and matches `assets/logo.svg`. Avoid adding undocumented fields or legacy Grok Build manifests to fix a Grok Bot installation issue.

The application also asks for organization name and handle, contact email, description, public GitHub repository, owner, and website. Submitting accepts the linked Publisher Terms; review and approve those terms before submitting.

## Before submission

1. Complete the package checks and authenticated Grok Bot connection/read/write smoke test in [testing.md](testing.md). Record any remaining acceptance checks explicitly for release follow-up.
2. Review the package, documentation, branding, and MIT licensing choice for public release.
3. Make the repository publicly accessible, as required by the marketplace, and verify the public URLs resolve.
4. Submit the repository URL through https://cursor.com/marketplace/publish and confirm the intended Grok Bot distribution.
5. Address reviewer feedback and verify the approved installation from a clean customer connection.
6. Replace development-preview language in the README with the verified listing URL and exact customer installation steps.

Marketplace plugins and updates undergo review. No approval date or Grok Bot listing is guaranteed by publishing this repository.

## Sources

- [Agent Plugins specification](https://agent-plugins.org/)
- [Cursor plugin reference](https://cursor.com/docs/reference/plugins)
- [Cursor marketplace security and review](https://cursor.com/help/security-and-privacy/marketplace-security)
- [Grok Bot plugin connection help](https://cursor.com/help/grok-bot/connect-plugins)
- [Quo plugin source](https://github.com/OpenPhone/quo-grok-plugin)

Quo's repository also includes files for Grok Build. Those files are not evidence of a Grok Bot local installation command. Supademo's package uses the standard hosted-server connection.
