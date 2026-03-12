---
name: lona-trading-strategy
description: Create and manage algorithmic trading strategies on the Lona platform. Use when the user wants to build a trading strategy, write Backtrader code, generate a strategy from a natural language description, list or inspect existing strategies, or update strategy code. Covers both manual Python strategy authoring and AI-powered strategy generation.
---

# Trading Strategy Development

You have access to Lona's trading strategy tools for creating and managing algorithmic trading strategies using the Backtrader framework.

## Available Tools

### Strategy Management
- **lona_list_strategies**: List all saved strategies with metadata (name, ID, description, version)
- **lona_get_strategy**: Get strategy details (name, description, version, language, timestamps)
- **lona_get_strategy_code**: View the Python Backtrader source code of a strategy
- **lona_create_strategy**: Create a new strategy from existing Python Backtrader code
- **lona_update_strategy**: Modify an existing strategy's name, description, or code. Returns a NEW strategy ID (versioning)

### AI Strategy Generation
- **lona_create_strategy_from_description**: Generate a strategy from a natural language description (async — returns jobId)
- **lona_get_strategy_creation_status**: Poll the async creation job for progress

## Strategy Code Requirements

All strategies must use Python with the Backtrader framework:
- Import: `import backtrader as bt`
- Inherit from `bt.Strategy`
- Define parameters using tuple format: `params = (('name', default_value),)`
- Implement `__init__` for indicators and `next` for trading logic
- Use `self.buy()`, `self.sell()`, `self.close()` for order execution
- Access data via `self.data.close[0]`, `self.data.open[0]`, etc.

## Workflows

### Create a strategy from Python code

1. Write Backtrader-compatible Python code
2. Call `lona_create_strategy` with name, description, and code
3. Receive a strategy ID for backtesting

### Generate a strategy with AI

1. Call `lona_create_strategy_from_description` with a clear natural language description
2. Receive a `jobId` immediately
3. Poll `lona_get_strategy_creation_status` every 10-15 seconds
4. Status pipeline: PENDING -> GENERATING -> SAVING -> COMPLETED/FAILED
5. When COMPLETED, receive the `strategyId`, generated code, explanation, and quality review
6. Typical creation time: 3-5 minutes

### Browse and inspect strategies

1. Call `lona_list_strategies` to see all saved strategies
2. Call `lona_get_strategy` with a strategy ID for metadata
3. Call `lona_get_strategy_code` to view the source code

### Update a strategy

1. Call `lona_update_strategy` with the strategy ID and new name, description, or code
2. Lona creates a new version — the returned ID is a new strategy

## Example Strategies

### Simple Moving Average Crossover
```python
import backtrader as bt

class SMACrossover(bt.Strategy):
    params = (
        ('fast_period', 10),
        ('slow_period', 30),
    )

    def __init__(self):
        self.fast_sma = bt.indicators.SMA(self.data.close, period=self.params.fast_period)
        self.slow_sma = bt.indicators.SMA(self.data.close, period=self.params.slow_period)
        self.crossover = bt.indicators.CrossOver(self.fast_sma, self.slow_sma)

    def next(self):
        if not self.position:
            if self.crossover > 0:
                self.buy()
        elif self.crossover < 0:
            self.close()
```

### RSI Mean Reversion
```python
import backtrader as bt

class RSIMeanReversion(bt.Strategy):
    params = (
        ('rsi_period', 14),
        ('oversold', 30),
        ('overbought', 70),
    )

    def __init__(self):
        self.rsi = bt.indicators.RSI(self.data.close, period=self.params.rsi_period)

    def next(self):
        if not self.position:
            if self.rsi[0] < self.params.oversold:
                self.buy()
        elif self.rsi[0] > self.params.overbought:
            self.close()
```

### Bollinger Band Breakout
```python
import backtrader as bt

class BollingerBreakout(bt.Strategy):
    params = (
        ('period', 20),
        ('devfactor', 2.0),
    )

    def __init__(self):
        self.bband = bt.indicators.BollingerBands(
            self.data.close, period=self.params.period, devfactor=self.params.devfactor
        )

    def next(self):
        if not self.position:
            if self.data.close[0] < self.bband.bot[0]:
                self.buy()
        elif self.data.close[0] > self.bband.top[0]:
            self.close()
```

## Tips

- Keep strategy descriptions detailed when using AI generation — mention indicators, entry/exit rules, position sizing, and risk management
- Use `lona_get_strategy_code` to review AI-generated code before backtesting
- Strategies support all standard Backtrader indicators (SMA, EMA, RSI, MACD, Bollinger Bands, ATR, etc.)
- Lona is for backtesting only, not live trading
