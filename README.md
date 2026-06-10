# Pipeworx for Cursor

Give Cursor one MCP that reaches **3,300+ live-data tools across 750+ sources** — SEC filings, USPTO patents, FRED, Census, FDA, EPA, USAspending, Polymarket, Zillow, weather, and 740+ more — without loading 3,300+ tool schemas into your context window every turn.

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

The plugin exposes **~26 meta-tools**, not all 3,300+ — `ask_pipeworx({question})` and friends route at runtime. This matters double in Cursor because Cursor re-sends every tool definition on every turn; a 3,300+-tool dump would dominate the context budget.

## Free tier + signup

100 calls/day anonymous, IP-bound. [Sign up free in 10s via GitHub](https://pipeworx.io/signup?via=cursor_plugin) for 200/day + a stable account.

## Verify after install

Open the MCP settings panel — `pipeworx` should show a green dot with ~26 tools. Then try in chat:

> What was the unemployment rate last month?

## What's loaded

- **`ask_pipeworx`** — natural-language router across all 750+ sources.
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

## Links

- Gateway: https://gateway.pipeworx.io
- Status: https://pipeworx.io/status
- Source: https://github.com/pipeworx-io/pipeworx

## License

MIT

---

⭐ Star if you'd use this — helps other Cursor users discover it.
