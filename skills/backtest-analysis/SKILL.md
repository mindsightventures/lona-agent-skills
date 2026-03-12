---
name: lona-backtest-analysis
description: Run backtests and analyze trading strategy performance on the Lona platform. Use when the user wants to test a strategy against historical data, check backtest results, view performance metrics like Sharpe ratio and drawdown, see trade history, or visualize trades on a chart.
---

# Backtest Execution & Analysis

You have access to Lona's backtesting tools for testing trading strategies against historical market data and analyzing the results.

## Available Tools

### Running Backtests
- **lona_run_backtest**: Execute a strategy against historical data (async — returns report_id immediately)
- **lona_get_report_status**: Poll the backtest execution status

### Viewing Results
- **lona_list_reports**: List all backtest reports with status and key metrics. Filter by `strategy_id` or `status`
- **lona_get_report**: Get summary metrics (total return, Sharpe ratio, max drawdown, win rate, trade count)
- **lona_get_full_report**: Comprehensive results with trade history, detailed metrics, and per-symbol breakdown
- **lona_get_report_chart**: Visualize trades on an interactive candlestick chart with buy/sell markers

## Workflows

### Run a backtest

Prerequisites: You need a `strategy_id` (from `lona_list_strategies` or `lona_create_strategy`) and one or more `data_ids` (from `lona_list_symbols` or `lona_download_market_data`).

1. Call `lona_run_backtest` with:
   - `strategy_id` (required)
   - `data_ids` array (required) — one or more symbol IDs
   - `start_date` and `end_date` in ISO format (required)
   - Optional: `initial_cash` (default: 100000), `commission` (default: 0.001), `leverage` (default: 1)
   - Optional: `parameters` object to override strategy params (e.g., `{"fast_period": 5, "slow_period": 20}`)
2. Receive `report_id` immediately
3. Poll `lona_get_report_status` every 5-10 seconds
4. Status pipeline: PENDING -> EXECUTING -> PROCESSING -> COMPLETED/FAILED
5. When COMPLETED, view results

### Analyze results

1. Call `lona_get_report` for a quick summary with key metrics
2. Call `lona_get_full_report` for the complete picture including trade-by-trade history
3. Call `lona_get_report_chart` to visualize entries and exits on a price chart

### Compare strategies

1. Call `lona_list_reports` to see all completed backtests
2. Get summary metrics for multiple reports with `lona_get_report`
3. Compare Sharpe ratios, drawdowns, and returns side by side

## Key Performance Metrics

| Metric | What It Measures | Good | Excellent |
|--------|------------------|------|-----------|
| **Total Return (%)** | Overall strategy profit/loss | > 0% | > 20% annually |
| **Sharpe Ratio** | Risk-adjusted return | > 1.0 | > 2.0 |
| **Max Drawdown (%)** | Largest peak-to-trough decline | < 20% | < 10% |
| **Win Rate (%)** | Percentage of profitable trades | > 50% | > 60% |
| **Number of Trades** | Statistical significance | > 30 | > 100 |
| **Net P&L ($)** | Absolute profit/loss | Positive | Consistent growth |
| **Profit Factor** | Gross profit / gross loss | > 1.5 | > 2.0 |

## Analysis Guidelines

### Red Flags
- Max drawdown > 30% — excessive risk, consider adding stop losses
- Win rate > 90% — likely overfitting or tiny take-profits with large stop losses
- Trade count < 10 — not statistically significant, test on longer periods
- Sharpe ratio < 0.5 — poor risk-adjusted returns, rethink the strategy logic

### Improvement Suggestions
- **Low Sharpe**: Add trend filters, tighten entry rules, or add position sizing
- **High drawdown**: Add stop losses, reduce position sizes, or add exit rules
- **Low win rate but profitable**: Normal for trend-following — ensure risk/reward ratio is favorable
- **High win rate but unprofitable**: Cut losses faster, the few losing trades are too large

### Multi-Instrument Analysis
When backtesting with multiple symbols:
- Use `lona_get_full_report` for per-symbol breakdown
- Check if performance is driven by one symbol or balanced across all
- Compare correlation between symbol returns
- Evaluate if diversification improved risk-adjusted metrics

## Examples

### Run a basic backtest
```
strategy_id: "abc123"
data_ids: ["def456"]
start_date: "2024-01-01"
end_date: "2024-12-31"
initial_cash: 100000
commission: 0.001
```

### Run with custom parameters
```
strategy_id: "abc123"
data_ids: ["def456", "ghi789"]
start_date: "2024-01-01"
end_date: "2024-12-31"
initial_cash: 50000
commission: 0.002
leverage: 2
parameters: {"fast_period": 5, "slow_period": 20, "stop_loss": 0.02}
```
