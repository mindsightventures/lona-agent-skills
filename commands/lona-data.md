---
name: lona-data
description: Browse and download market data for backtesting
---

# Lona Market Data

Browse available market data and download new data from exchanges.

## Actions

### Browse available data
- `lona_list_symbols` - List user's uploaded data
- `lona_list_symbols` with `is_global: true` - List pre-loaded global datasets
- `lona_get_symbol` - Get symbol details (exchange, asset class, frequency)
- `lona_get_symbol_data` - Preview OHLCV price data

### Download from Binance
Use `lona_download_market_data` with:
- **symbol**: Binance pair (BTCUSDT, ETHUSDT, SOLUSDT, etc.)
- **interval**: 1m, 5m, 15m, 30m, 1h, 4h, 1d
- **start_date** / **end_date**: ISO date format

Returns a `symbol_id` ready for use with `lona_run_backtest`.

### Practical limits
- 1m data: ~6 months
- 5m data: ~2 years
- 1h+ data: several years

## Ask the user
- What data they're looking for
- Which symbol/pair and exchange
- What timeframe and date range
