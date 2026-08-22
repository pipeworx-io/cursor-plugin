# Pipeworx for Cursor

Give Cursor one MCP that reaches **5,581+ live-data tools across 1,463+ sources** — SEC filings, USPTO patents, FRED, Census, FDA, EPA, USAspending, Polymarket, Zillow, weather, and 1,455+ more — without loading 5,581+ tool schemas into your context window every turn.

## Install

From the Cursor Marketplace:

```text
cursor.com/marketplace → search "pipeworx" → Install
```

Or one-click via deeplink:

```text
cursor://anysphere.cursor-deeplink/plugin/install?name=pipeworx
```

## Try it

After install, ask Cursor things like:

| Ask | What it triggers |
|---|---|
| *"What just happened to Apple?"* | `sec_8k_recent` → SEC 8-K events classified by severity |
| *"Spread between Polymarket and Kalshi on the next Fed decision?"* | `polymarket_kalshi_spread` → live cross-venue mispricing |
| *"Overdue Phase 3 readouts at Moderna?"* | `pharma_pipeline_catalysts` → biotech catalyst calendar |
| *"DoD cybersecurity contracts this week?"* | `usa_award_search` → sub-second USAspending mirror |
| *"Median home value and renter share in Lubbock, TX?"* | `housing_market_snapshot` + `housing_metro_demand` |
| *"Unemployment rate last month?"* | `fred_get_series` → official FRED data |

Cursor picks the right tool via `ask_pipeworx` — no pack-name memorization required.

## How it loads light

The plugin exposes **~31 meta-tools**, not all 5,581+ — `ask_pipeworx({question})` and friends route at runtime. This matters double in Cursor because Cursor re-sends every tool definition on every turn; a 5,581+-tool dump would dominate the context budget.

## Free tier + signup

50 calls/day anonymous, IP-bound. [Sign up free in 10s via GitHub](https://pipeworx.io/signup?via=cursor_plugin) for 200/day + a stable account.

## Verify after install

Open the MCP settings panel — `pipeworx` should show a green dot with ~38 tools. Then try in chat:

> What was the unemployment rate last month?

## What's loaded

- **`ask_pipeworx`** — natural-language router across all 1,463+ sources.
- **`discover_tools`** — top-20 relevant tools for a task, with full schemas.
- **`entity_profile`** / **`compare_entities`** / **`recent_changes`** / **`resolve_entity`** — fan-out across multiple packs in one call.
- **`validate_claim`** — fact-check claims against SEC XBRL.
- **`remember`** / **`recall`** / **`forget`** — persistent memory across sessions.
- **`list_packs`** / **`search_packs`** / **`get_pack_tools`** / **`get_connection_config`** / **`get_platform_status`** / **`search_mcp_directory`** — browse the catalog.

The bundled skill + always-on rule teach Cursor when to reach for each.

## Direct pack access

For a specific pack's tools loaded directly (e.g., `attom_property_search` without going through `ask_pipeworx`), add a scoped entry to your project's `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "pipeworx-attom": {
      "url": "https://gateway.pipeworx.io/attom/mcp"
    }
  }
}
```

Or a vertical bundle (e.g., `?vertical=housing` for the housing-data stack).

## Bring your own key

For BYO-tier limits (200/day) or to attach your own per-tool API keys, add an `X-API-Key` header in `mcp.json`:

```json
{
  "mcpServers": {
    "pipeworx": {
      "url": "https://gateway.pipeworx.io/pipeworx-catalog/mcp",
      "headers": { "X-API-Key": "YOUR_KEY_HERE" }
    }
  }
}
```

**No key? Sign in instead — it is free and gets you the same 200 calls/day.**
Use `https://gateway.pipeworx.io/oauth/mcp` as the `url` with no `headers` block,
and complete the GitHub sign-in when Cursor prompts. Keep the anonymous URL
(`.../pipeworx-catalog/mcp`, no headers) if you want no account at all — that is
50 calls/day. Note the two are alternatives: an `X-API-Key` sent to the OAuth URL
is rejected, because that endpoint authenticates with a bearer token.

## Links

- Gateway: https://gateway.pipeworx.io
- Status: https://pipeworx.io/status
- Source: https://github.com/pipeworx-io/pipeworx

## License

MIT

---

⭐ Star if you'd use this — helps other Cursor users discover it.
