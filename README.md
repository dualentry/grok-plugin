# DualEntry plugin for Grok Build

Connect Grok to the live DualEntry ledger. The plugin bundles DualEntry's hosted MCP server. After install, Grok can search records, resolve entities, and draft accounting changes with the same permissions as the DualEntry dashboard.

The hosted MCP is the only runtime path. There is no local server and no API key to paste.

## Features

- Search invoices, bills, journal entries, and other records
- Resolve vendors, customers, accounts, companies, and items
- Inspect history, related payments, and bank-match suggestions
- Preview and create contracts and fixed assets
- Save records and entities after the user confirms the payload

## Install

You need [xAI Grok Build](https://docs.x.ai/build/overview), not Homebrew `grok`.
Homebrew grok is a log parser (`Usage: grok [-d] <-f config_file>`). It does not
support MCP.

```bash
curl -fsSL https://x.ai/cli/install.sh | bash
```

### Grok Build marketplace

In Grok Build, run `/marketplace`, search for **dualentry**, and install it.

Or from the terminal:

```bash
grok plugin install dualentry --trust
```

### Manual MCP add

```bash
grok mcp add --transport http dualentry https://api.dualentry.com/mcp/
```

`grok mcp doctor dualentry` fails with **Auth required** until you sign in. Run `grok`, then `/mcps`, select `dualentry`, press `i`. Doctor does not open OAuth.

### grok.com custom connector

1. Open [grok.com/connectors](https://grok.com/connectors).
2. Click **New Connector**, then **Custom**.
3. Enter `https://api.dualentry.com/mcp/`.
4. Complete DualEntry sign-in in the browser.

## Sign in

The first DualEntry tool call opens a browser for DualEntry OAuth. Approve once. Grok stores the token in `~/.grok/mcp_credentials.json`. Do not paste an API key into Grok or into the connector URL.

If `grok mcp doctor` says `handshake failed` / `Auth required`, DualEntry is up. Doctor skipped OAuth. Authenticate with `/mcps` then `i`.

## Usage

Ask in plain language:

```text
Show unpaid invoices over $10,000 this quarter.
```

```text
What payments sit against invoice IN-1204?
```

```text
Find the vendor "Acme Supplies" and list open bills.
```

## Server URL

| Environment | URL |
|---|---|
| Production | `https://api.dualentry.com/mcp/` |
| Development | `https://api-dev.dualentry.com/mcp/` |

Auth uses OAuth 2.1 with PKCE and dynamic client registration. See [MCP integration](https://docs.dualentry.com/developers/guides/mcp-integration).

## Support

- Docs: https://docs.dualentry.com/developers/guides/mcp-integration
- Product: https://dualentry.com
- Email: support@dualentry.com

Source: [github.com/dualentry/grok-plugin](https://github.com/dualentry/grok-plugin)
