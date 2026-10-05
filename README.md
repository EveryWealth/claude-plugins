# EveryWealth plugins for Claude

Official [Claude Code](https://claude.com/claude-code) plugin marketplace for
[EveryWealth](https://everywealth.com.au). Query your live portfolio from
Claude: organisation snapshots, investments, transactions, source and
governance documents, live market data, and free-form portfolio Q&A.
Read-only.

## Install

```bash
claude plugin marketplace add EveryWealth/claude-plugins
```

```bash
claude plugin install investsync@investsync-plugins
```

The first time Claude uses an EveryWealth tool, run `/mcp`, choose
**Authenticate**, and approve access in your browser on an EveryWealth page.
You choose one organisation or all of yours. There are no keys to copy.

Full setup and the list of tools are in
[plugins/investsync-mcp/README.md](plugins/investsync-mcp/README.md).

## Prefer no plugin?

Register the MCP server directly, then authenticate with `/mcp`:

```bash
claude mcp add --transport http investsync https://app.everywealth.com.au/api/mcp
```

Claude on the web or desktop and ChatGPT connect to the same address as a
custom connector. See **Settings → Integrations** in EveryWealth.

## About this repository

This repository is a read-only mirror, synced automatically from the
EveryWealth monorepo. Issues are welcome, but pull requests here will be
overwritten by the next sync.
