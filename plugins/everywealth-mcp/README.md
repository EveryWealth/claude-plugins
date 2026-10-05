# EveryWealth MCP plugin

Connects Claude Code (and any MCP-capable client) to your live EveryWealth
organisation, read-only.

> Maintainers: see [PUBLISHING.md](PUBLISHING.md) for how to deploy the server
> and distribute this plugin to users (marketplaces, community submission,
> other Claude surfaces).

## Setup

Install the plugin — that's it:

```bash
claude plugin marketplace add EveryWealth/claude-plugins
```

```bash
claude plugin install everywealth@everywealth-plugins
```

The first time Claude uses an EveryWealth tool it will ask you to authenticate:
run `/mcp`, choose **Authenticate**, and approve access in your browser on an
EveryWealth page (you choose one organisation or all of yours). No tokens to
copy. You can also start from **Settings → Integrations → Claude** inside
EveryWealth.

For local development against `next dev`, point the plugin at your dev server:

```bash
export EVERYWEALTH_MCP_URL="http://localhost:3000/api/mcp"
```

### Headless / CI: pre-issued token

For scripts or clients without a browser, mint a personal access token from
**Settings → Integrations → Claude** (or `POST /api/mcp/token`; org-scoped by
default, `{"scope":"user"}` for all your organisations) and register the
server with a header instead of installing the plugin:

```bash
claude mcp add --transport http everywealth https://app.everywealth.com.au/api/mcp --header "Authorization: Bearer $EVERYWEALTH_MCP_TOKEN"
```

## Tools

| Tool | What it does |
| --- | --- |
| `list_organisations` | Your organisations and which ones this connection can query |
| `get_organisation_snapshot` | Portfolio totals, movement, top holdings, categories, tags for a period |
| `list_investments` | All investments with value, cost basis, units, category, lifecycle |
| `get_investment` | Detailed single-investment view by shortCode, incl. source document links |
| `query_transactions` | Filtered, paginated transaction history with source document links |
| `list_documents` | Stored source documents (statements, contract notes) with links |
| `search_reference_documents` | Search governance documents (constitutions, trust deeds, policies) with clause and page citations |
| `list_document_records` | Governance document records with their current version and links |
| `search` / `fetch` | One-query search across the snapshot, investments and governance documents, then full content by id (the shape ChatGPT deep research uses) |
| `ask_portfolio` | Free-form question answered by the EveryWealth portfolio analyst |
| `market_data` | Live listed-market data via Steady: search, quote, summary, price history |

Every tool accepts an optional `organisation` argument (id, slug, or name)
when your connection covers more than one organisation.

Access is read-only and membership is re-checked on every request — removing a
member revokes their access immediately. Document links open through the
app's authenticated download route, so they only work in a browser signed in
to the organisation.
