---
name: lona-backtest
description: Run a complete backtest workflow from strategy to results
---

# Lona Backtest Workflow

Execute a complete backtesting workflow: select or create a strategy, ensure market data is available, run the backtest, and analyze results.

## Steps

1. **Check existing strategies** - Use `lona_list_strategies` to see available strategies
2. **Select or create strategy** - Either pick an existing strategy or create a new one:
   - From code: `lona_create_strategy`
   - From description: `lona_create_strategy_from_description` (async, poll with `lona_get_strategy_creation_status`)
3. **Check market data** - Use `lona_list_symbols` to see available data
4. **Download data if needed** - Use `lona_download_market_data` to get data from Binance
5. **Run backtest** - Use `lona_run_backtest` with the strategy ID and data IDs
6. **Monitor progress** - Poll `lona_get_report_status` every 5-10 seconds until COMPLETED or FAILED
7. **View results** - Use `lona_get_report` for summary or `lona_get_full_report` for detailed analysis
8. **Visualize trades** - Use `lona_get_report_chart` to see trade entries/exits

## Ask the user

- Which strategy to test (or describe one to create)
- Which market/symbol to test on
- What date range to backtest
- Any specific parameters (initial cash, commission, leverage)
