# Talval MCP server

[![M8ven Score](https://m8ven.ai/badge/mcp/talval-research-talval-mcp-1902gq?v=36c52c68177d765a13724589ae57859e&variant=verified)](https://m8ven.ai/mcp/talval-research-talval-mcp-1902gq?s=readme)

Value-investing research on public companies, as tools your agent can call.

**Hosted. Nothing to install, no API key, no account.** Point your MCP client at
`https://talval.com/mcp` and the tools appear.

```
https://talval.com/mcp
```

---

## What it answers

Ask your assistant *"is Apple undervalued?"* and it can now check rather than
recall:

```
# Apple Inc. (AAPL) — Talval research

**Verdict:** Fairly valued · conviction 7/10 · risk Medium
Snapshot date: 2026-09-28

- Last close: 341 USD (as of 2026-09-25)
- Fair value estimate: 397 USD
- Upside to fair value: +16%
- Trailing P/E: 45.7

## Scores (0-100)
- Value: 0/100   - Quality: 90/100   - Safety: 61/100
- Dividend: 52/100   - Composite: 63/100   - Piotroski F-score: 8/9

## Filed results, fiscal 2025
- Revenue: 416.2B USD      - Net income: 112.0B USD
- Free cash flow: 98.8B USD  - Diluted EPS: 7.46 USD
As reported in the company's own filings — not estimates.
```

That is a real response, not a mock-up. Every figure carries the date it was
taken, and filed results are separated from estimates, because an agent that
cannot tell the two apart will present a model's guess as a fact.

## Tools

| Tool | What it does |
|---|---|
| `search_stocks` | Find a company by name or ticker. Typo tolerant — use it first when you only have a name. |
| `get_stock_research` | Verdict, fair-value estimate, upside, quality/safety/value scores and latest filed results for one ticker. End-of-day snapshot with a date. |
| `compare_stocks` | Two to eight tickers side by side on verdict, fair value, upside and scores. |
| `screen_stocks` | Run a screen over the covered universe: `undervalued`, `high_quality`, `safe_dividend`, `undervalued_dividend`. Optional sector filter. |
| `list_superinvestors` | The investors tracked through quarterly 13F filings — portfolio size, position count, largest holdings. |
| `get_superinvestor` | One investor's reported holdings and quarter-on-quarter activity. |
| `stocks_of_the_week` | The current weekly picks — latest Undervalued verdict per ticker. |

Coverage is US and European listed companies. Tickers are exactly as Talval
lists them: `AAPL`, `RHM.DE`, `PRU.L`.

## Connect it

### Claude Desktop

`claude_desktop_config.json` — see [examples/claude-desktop.json](examples/claude-desktop.json):

```json
{
  "mcpServers": {
    "talval": {
      "type": "url",
      "url": "https://talval.com/mcp"
    }
  }
}
```

### Claude Code

```bash
claude mcp add --transport http talval https://talval.com/mcp
```

### Cursor

`.cursor/mcp.json` — see [examples/cursor.json](examples/cursor.json):

```json
{
  "mcpServers": {
    "talval": {
      "url": "https://talval.com/mcp"
    }
  }
}
```

### Anything else

Streamable HTTP at `https://talval.com/mcp`. The server card is published at
[`/.well-known/mcp.json`](https://talval.com/.well-known/mcp.json) and mirrored
here as [`server.json`](server.json).

This repository is also an [Agent Plugin](https://agent-plugins.org): the root
carries [`plugin.json`](plugin.json) and [`mcp.json`](mcp.json), so a client or
directory that reads that standard can pick the server up without being told
where to look.

## Two endpoints

| Endpoint | Auth | What you get |
|---|---|---|
| `https://talval.com/mcp` | none | Everything listed above |
| `https://talval.com/mcp/pro` | OAuth | The same, on a subscriber's own plan limits |

The free endpoint is not a teaser: verdicts, fair values, scores, screens and
13F portfolios all work without an account. What sits behind a subscription —
institutional ownership and insider flow, long-term outlook scenarios, analyst
consensus and the written investment thesis — is named in each response rather
than silently omitted, with a link to the page that has it.

## What this repo is

Documentation and connection config for a **hosted** server. There is no package
to install and no source to build here; the service runs at talval.com. The repo
exists so the server can be found, described and registered the way MCP clients
and directories expect.

## Honest limits

- **End-of-day, not live.** Prices and snapshots carry the date they were taken.
- **Coverage is a universe, not the market.** If `search_stocks` returns nothing,
  that company is not covered — the server says so rather than guessing.
- **Scores can be `n/a`.** Where the filings behind a figure are missing, the
  field is blank instead of filled with a default. A blank means "not known",
  and that is deliberately visible.
- **Verdicts are model output.** They are a starting point for research, not a
  recommendation — see below.

## Not investment advice

Talval publishes research, not advice. Verdicts and fair-value estimates are
model outputs for information only, and nothing here is a recommendation to buy
or sell anything. Do your own work.

---

[talval.com](https://talval.com) · [company pages](https://talval.com/company/AAPL) ·
[how it works](https://talval.com/about) · [screens](https://talval.com/screener/undervalued-stocks)
