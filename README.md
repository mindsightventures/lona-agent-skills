# Lona Trading Platform — Claude Plugin

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-2.0.0-green.svg)](CHANGELOG.md)
[![Claude Code](https://img.shields.io/badge/Claude-Code-blueviolet)](https://code.claude.com)
[![Claude Cowork](https://img.shields.io/badge/Claude-Cowork-blueviolet)](https://claude.com)

AI-powered algorithmic trading strategy development plugin for [Claude Code](https://code.claude.com) and [Claude Cowork](https://claude.com). Create, backtest, and analyze trading strategies using the [Lona platform](https://www.lona.agency).

## Quick Start

### Install as Claude Code Plugin

```bash
# From the Plugin Directory (when available)
claude plugin add lona

# Or install directly from GitHub
claude plugin add https://github.com/mindsightventures/lona-agent-skills
```

### Try It

```
/lona-backtest
```

This walks you through creating a strategy, downloading data, running a backtest, and analyzing results — all in one workflow.

## What's Included

### Skills

Domain-specific knowledge that Claude loads on-demand when relevant.

| Skill | Description |
|-------|-------------|
| [trading-strategy](./trading-strategy/SKILL.md) | Create and manage Backtrader strategies — from Python code or natural language descriptions |
| [market-data](./market-data/SKILL.md) | Browse pre-loaded datasets (equities, crypto, forex) and download from Binance |
| [backtest-analysis](./backtest-analysis/SKILL.md) | Run backtests and analyze performance — Sharpe ratio, drawdown, win rate, trade history |

### Slash Commands

Quick-access workflows invoked with `/lona:command-name`.

| Command | Description |
|---------|-------------|
| [/lona-backtest](./commands/lona-backtest.md) | Full end-to-end: strategy + data + backtest + results |
| [/lona-strategies](./commands/lona-strategies.md) | List, create, view, and update strategies |
| [/lona-data](./commands/lona-data.md) | Browse symbols and download market data |

### Agent

| Agent | Description |
|-------|-------------|
| [trading-assistant](./agents/trading-assistant.md) | Specialized agent for trading strategy development and analysis |

## MCP Tools (18 total)

This plugin connects to the Lona MCP Server, which provides 18 tools:

| Category | Tools |
|----------|-------|
| **Strategy Management** | `lona_list_strategies`, `lona_get_strategy`, `lona_get_strategy_code`, `lona_create_strategy`, `lona_update_strategy` |
| **AI Generation** | `lona_create_strategy_from_description`, `lona_get_strategy_creation_status` |
| **Market Data** | `lona_list_symbols`, `lona_get_symbol`, `lona_get_symbol_data`, `lona_download_market_data` |
| **Backtesting** | `lona_run_backtest`, `lona_get_report_status` |
| **Reports** | `lona_list_reports`, `lona_get_report`, `lona_get_full_report`, `lona_get_report_chart` |
| **Auth** | `lona_register_agent` |

## Configuration

The plugin connects to Lona via MCP. The `.mcp.json` configuration:

```json
{
  "mcpServers": {
    "lona": {
      "command": "npx",
      "args": ["@lona/mcp-server"],
      "env": {
        "LONA_GATEWAY_URL": "https://gateway.lona.agency",
        "LONA_API_KEY": "your-api-key",
        "LONA_USER_ID": "your-user-id"
      }
    }
  }
}
```

Get your API key and User ID from [lona.agency](https://www.lona.agency).

For OAuth-based connections (Claude.ai Connectors), the MCP endpoint is:
- **URL**: `https://mcp.lona.agency/mcp`
- **Auth**: OAuth 2.1 with PKCE

## Example Workflows

### 1. Generate a strategy from a description
> "Create a momentum strategy that buys when RSI crosses below 30 and sells above 70"

Claude uses the trading-strategy skill to call `lona_create_strategy_from_description`, polls until the code is generated, and presents the Python source for review.

### 2. Download data and run a backtest
> "/lona-backtest" → Select strategy → Download BTCUSDT daily data → Run with $100K → View results

Full E2E workflow with Sharpe ratio, max drawdown, win rate, and trade-by-trade history.

### 3. Compare strategy performance
> "List my recent backtest reports and compare the top 3 by Sharpe ratio"

Claude uses the backtest-analysis skill to fetch reports, extract metrics, and provide side-by-side analysis.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on reporting issues, submitting PRs, and adding skills.

## About

[Lona](https://www.lona.agency) is an AI-powered trading strategy development platform by [Mindsight Ventures](https://mindsightventures.ai).

## License

[MIT](LICENSE)
