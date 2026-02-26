# Lona Agent Skills

Agent Skills for the [Lona Trading Platform](https://www.lona.agency) — AI-powered algorithmic trading strategy development, backtesting, and analysis.

These skills extend Claude's capabilities with domain expertise for trading strategy development using Lona's MCP tools.

## Skills

| Skill | Description |
|-------|-------------|
| [trading-strategy](./trading-strategy/SKILL.md) | Create and manage algorithmic trading strategies — write Backtrader code or generate strategies from natural language |
| [market-data](./market-data/SKILL.md) | Browse pre-loaded datasets and download cryptocurrency data from Binance |
| [backtest-analysis](./backtest-analysis/SKILL.md) | Run backtests against historical data and analyze performance metrics |

## Requirements

These skills are designed to work with the **Lona MCP Server**. You need an active Lona MCP connection to use them.

### On Claude.ai

Connect the Lona MCP server via the Connectors Directory or manually add:
- **MCP Endpoint**: `https://mcp.lona.agency/mcp`
- **Authentication**: OAuth 2.1

### On Claude Code

Add the MCP server to your configuration:

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

## Installation

### Claude Code (via skills directory)

```bash
git clone https://github.com/mindsightventures/lona-agent-skills.git ~/.claude/skills/lona
```

### Claude.ai

Upload skills as zip files through Settings > Features.

### Claude API

Upload via the Skills API (`/v1/skills` endpoints).

## Full Workflow Example

A typical workflow combines all three skills:

1. **Create a strategy** (trading-strategy skill): "Create a strategy that buys when RSI crosses below 30 and sells above 70"
2. **Get market data** (market-data skill): "Download daily BTCUSDT data for 2024"
3. **Run backtest** (backtest-analysis skill): "Backtest the strategy on the downloaded data with $100K initial capital"
4. **Analyze results** (backtest-analysis skill): "Show me the full report with trade history and the chart"

## About Lona

[Lona](https://www.lona.agency) is an AI-powered trading strategy development platform. Create, backtest, and analyze algorithmic trading strategies using Python Backtrader. Download market data from Binance, generate strategies with AI, and view detailed performance reports.

**Developer**: [Mindsight Ventures](https://www.mindsightventures.com)

## License

MIT
