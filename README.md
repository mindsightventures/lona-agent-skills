# LONA Trading Assistant — Plugin

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-2.1.0-green.svg)](CHANGELOG.md)
[![MCP Registry](https://img.shields.io/badge/MCP-Registry-blue)](https://registry.modelcontextprotocol.io/)
[![Claude Code](https://img.shields.io/badge/Claude-Code-blueviolet)](https://code.claude.com)
[![Cursor](https://img.shields.io/badge/Cursor-Marketplace-orange)](https://cursor.com/marketplace)

AI-powered algorithmic trading strategy development plugin for [Claude Code](https://code.claude.com), [Claude Cowork](https://claude.com), and [Cursor](https://cursor.com). Create, backtest, and analyze trading strategies using the [Lona platform](https://www.lona.agency).

## Quick Start

### Install in Cursor

```bash
# From the Cursor Marketplace (when available)
cursor://anysphere.cursor-deeplink/mcp/install?name=lona
```

Or add the MCP server manually in Cursor Settings → Features → MCP:

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

### Install in Claude Code

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

Domain-specific knowledge loaded on-demand when relevant.

| Skill | Description |
|-------|-------------|
| [trading-strategy](./skills/trading-strategy/SKILL.md) | Create and manage Backtrader strategies — from Python code or natural language descriptions |
| [market-data](./skills/market-data/SKILL.md) | Browse pre-loaded datasets (equities, crypto, forex) and download from Binance |
| [backtest-analysis](./skills/backtest-analysis/SKILL.md) | Run backtests and analyze performance — Sharpe ratio, drawdown, win rate, trade history |

### Rules (Cursor)

| Rule | Description |
|------|-------------|
| [lona-trading](./rules/lona-trading.mdc) | Guidelines for using Lona MCP tools to develop and backtest trading strategies |

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

## Platform Compatibility

| Platform | Status | Components |
|----------|--------|------------|
| **Cursor** | Marketplace (pending review) | Skills, Rules, Agents, Commands, MCP |
| **Claude Code** | Plugin Directory | Skills, Agents, Commands, MCP |
| **Claude.ai (Cowork)** | MCP Connectors | MCP Tools + Widgets |
| **ChatGPT** | App Store (pending review) | MCP Tools + Widgets |
| **MCP Registry** | Published (`agency.lona/trading`) | MCP Server |

## Example Workflows

### 1. Generate a strategy from a description
> "Create a momentum strategy that buys when RSI crosses below 30 and sells above 70"

The AI generates Backtrader Python code based on the description, polls until complete, and presents the source for review.

### 2. Download data and run a backtest
> "/lona-backtest" → Select strategy → Download BTCUSDT daily data → Run with $100K → View results

Full E2E workflow with Sharpe ratio, max drawdown, win rate, and trade-by-trade history.

### 3. Compare strategy performance
> "List my recent backtest reports and compare the top 3 by Sharpe ratio"

Fetches reports, extracts metrics, and provides side-by-side analysis.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on reporting issues, submitting PRs, and adding skills.

## About

[Lona](https://www.lona.agency) is an AI-powered trading strategy development platform by [Mindsight Ventures](https://mindsightventures.ai).

## License

[MIT](LICENSE)
