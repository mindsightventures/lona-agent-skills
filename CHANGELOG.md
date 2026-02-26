# Changelog

All notable changes to this project will be documented in this file.

## [2.0.0] - 2026-02-26

### Added

- Initial public release of the Lona Agent Skills plugin
- **Skills**:
  - `lona-trading-strategy` — Create and manage Backtrader strategies + AI generation
  - `lona-market-data` — Browse datasets and download crypto data from Binance
  - `lona-backtest-analysis` — Run backtests and analyze performance metrics
- **Commands**:
  - `/lona-backtest` — Full end-to-end backtest workflow
  - `/lona-strategies` — Strategy CRUD operations
  - `/lona-data` — Market data browsing and download
- **Agent**:
  - `trading-assistant` — Specialized agent for trading strategy development
- Plugin manifest (`.claude-plugin/plugin.json`)
- MCP server connection (`.mcp.json`) via `npx @lona/mcp-server`
