# Partner and Member Directory Extractor MCP Server

[![Smithery](https://smithery.ai/badge/mambabuilt/mcp-partner-member-directory-extractor)](https://smithery.ai/servers/mambabuilt/mcp-partner-member-directory-extractor) [![Glama score](https://glama.ai/mcp/servers/mambalabsdev/mcp-partner-member-directory-extractor/badges/score.svg)](https://glama.ai/mcp/servers/mambalabsdev/mcp-partner-member-directory-extractor) [![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-partner-member-directory-extractor%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-partner-member-directory-extractor&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-partner-member-directory-extractor)](https://www.npmjs.com/package/@mambalabsdev/mcp-partner-member-directory-extractor) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-partner-member-directory-extractor)](https://www.npmjs.com/package/@mambalabsdev/mcp-partner-member-directory-extractor) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-partner-member-directory-extractor)](https://github.com/mambalabsdev/mcp-partner-member-directory-extractor/blob/main/LICENSE) [![mcpservers.org](https://img.shields.io/badge/mcpservers.org-listed-blue)](https://mcpservers.org/servers/mambalabsdev/mcp-partner-member-directory-extractor)

<a href="https://mcprush.com/to/partner-member-directory-extractor-mcp?ref=badge"><img width="380" height="200" src="https://mcprush.com/badge/partner-member-directory-extractor-mcp/card.svg" alt="Partner Member Directory Extractor MCP server" /></a>

An MCP server for the Mamba Labs Partner and Member Directory Extractor actor on Apify. Give it a partner directory or a member list URL. Each listed company comes back as one row with its website, domain, tier, tags, and location.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Your keys](#your-keys)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

The actor reads three directory families: directories built on PartnerPage (Clay's Solutions Partner Directory and the Zapier partner directory among them), read through PartnerPage's public listing API; the Shopify Partner Directory; and member lists that link to one profile page per member, such as a trade association directory. Each row carries `listing_name`, `company_domain`, `website`, `listing_url`, `tier`, `tags`, `location`, `rating`, `review_count`, `partner_since`, and the `listed_email` and `listed_phone` the directory publishes. robots.txt is checked before every request. A directory that builds its list in the browser returns one free row with `row_status` `unsupported`.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-partner-member-directory-extractor": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-partner-member-directory-extractor"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `extract_directory_companies` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "List every agency in the Clay experts directory with its website and tier."
- "Pull 100 Shopify partners that do store migrations, with their rating and location."
- "Turn the IAB UK member directory into a list of company domains."

## Tool

`extract_directory_companies`. One tool. Example arguments:

```json
{
  "directory_url": "https://www.clay.com/en/experts",
  "max_listings": "200"
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults. Numbers and yes or no inputs are sent as text.

| Input | Type | Description |
|---|---|---|
| `directory_url` | string | One directory page |
| `directory_urls` | array | Up to 20 directory pages |
| `max_listings` | string | Listings per directory, 1 to 5000. Default 100 |
| `max_pages` | string | Shopify and member lists: listing pages to read. Default 10 |
| `include_details` | string | PartnerPage: tags, location, and email. Default true |
| `dedupe_domains` | string | Return a repeated company once. Default true |
| `max_charge_usd` | string | Optional cost cap for the run |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `company-listed`, per company row | $0.004 | $0.0038 | $0.0036 | $0.0034 |
| `apify-actor-start`, per run start (one per GB of run memory) | $0.0015 | $0.0015 | $0.0015 | $0.0015 |

Skipped repeats, and no listings, robots disallowed, blocked, unsupported, and error rows are free.

## Your keys

The actor needs no key. Proxy traffic adds nothing to your price: Mamba Labs pays the platform costs of the run.

## Full actor documentation

[apify.com/mambalabs/partner-member-directory-extractor](https://apify.com/mambalabs/partner-member-directory-extractor)

## License

MIT. See [LICENSE](LICENSE).
