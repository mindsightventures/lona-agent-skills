---
name: lona-market-data
description: Browse, download, and manage market data for algorithmic trading backtests on the Lona platform. Use when the user wants to find available market data, download cryptocurrency data from Binance, inspect OHLCV time-series, or check what data is available for backtesting.
---

# Market Data Management

You have access to Lona's market data tools for browsing available datasets and downloading new data from cryptocurrency exchanges.

## Available Tools

### Browsing Data
- **lona_list_symbols**: List available market data. Use `is_global: true` for pre-loaded datasets (US equities, crypto, forex) or `is_global: false` for user-uploaded/downloaded data
- **lona_get_symbol**: Get symbol details (name, exchange, asset class, frequency, quote currency, date range)
- **lona_get_symbol_data**: Preview OHLCV time-series data (Open, High, Low, Close, Volume)

### Downloading Data
- **lona_download_market_data**: Download cryptocurrency data from Binance. Returns a symbol ID for immediate use in backtests

## Data Types

Symbols contain OHLCV (Open, High, Low, Close, Volume) time-series data:
- **Global data** (`is_global: true`): Pre-loaded datasets available to all users — includes US equities, major cryptocurrencies, and forex pairs
- **User data** (`is_global: false`): Data downloaded or uploaded by the user

## Workflows

### Find available data

1. Call `lona_list_symbols` with `is_global: true` to browse pre-loaded datasets
2. Call `lona_list_symbols` without `is_global` to see user's own data
3. Use `lona_get_symbol` for detailed metadata on a specific symbol
4. Use `lona_get_symbol_data` to preview the actual OHLCV data points

### Download cryptocurrency data from Binance

1. Call `lona_download_market_data` with:
   - `symbol`: Binance spot pair (e.g., `BTCUSDT`, `ETHUSDT`, `SOLUSDT`)
   - `interval`: Candle interval (see supported intervals below)
   - `start_date` and `end_date` in ISO format (optional — defaults vary by interval)
   - `limit`: Maximum number of candles (optional)
2. Data downloads and processes automatically
3. Returns a `symbol_id` for immediate use with `lona_run_backtest`

### Supported Binance Intervals

| Interval | Code | Practical Limit |
|----------|------|-----------------|
| 1 minute | `1m` | ~6 months |
| 5 minutes | `5m` | ~2 years |
| 15 minutes | `15m` | ~3 years |
| 30 minutes | `30m` | ~3 years |
| 1 hour | `1h` | Several years |
| 4 hours | `4h` | Several years |
| 1 day | `1d` | Several years |

### Common Binance Symbols

Major cryptocurrencies: `BTCUSDT`, `ETHUSDT`, `BNBUSDT`, `SOLUSDT`, `XRPUSDT`, `DOGEUSDT`, `ADAUSDT`, `AVAXUSDT`, `DOTUSDT`, `MATICUSDT`

## Examples

### Download daily Bitcoin data for 2024
```
symbol: "BTCUSDT"
interval: "1d"
start_date: "2024-01-01"
end_date: "2024-12-31"
```

### Download hourly Ethereum data for the last 3 months
```
symbol: "ETHUSDT"
interval: "1h"
start_date: "2025-11-26"
end_date: "2026-02-26"
```

## Data Quality Tips

- Higher timeframes (1h, 4h, 1d) are more reliable for backtesting
- 1-minute data has practical API limits (~6 months maximum)
- Always verify downloaded data with `lona_get_symbol_data` to confirm date range and quality
- Check pre-loaded global datasets first before downloading — they may already have what you need
- For multi-instrument strategies, download all symbols at the same interval and overlapping date ranges
