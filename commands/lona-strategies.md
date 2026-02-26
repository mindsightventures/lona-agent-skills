---
name: lona-strategies
description: List, create, and manage trading strategies
---

# Lona Strategy Management

Manage trading strategies on the Lona platform.

## Actions

### List strategies
Use `lona_list_strategies` to show all saved strategies with their names, IDs, and versions.

### View strategy details
Use `lona_get_strategy` to get metadata, then `lona_get_strategy_code` to view the Python source code.

### Create from code
Use `lona_create_strategy` with Python Backtrader code. The code must:
- Import backtrader (`import backtrader as bt`)
- Define a class inheriting from `bt.Strategy`
- Use params tuple format: `params = (('name', default),)`

### Create from description
Use `lona_create_strategy_from_description` for AI-powered generation:
1. Provide a natural language description
2. Poll `lona_get_strategy_creation_status` every 10-15 seconds
3. Wait for COMPLETED status (typically 3-5 minutes)

### Update strategy
Use `lona_update_strategy` to modify name, description, or code of an existing strategy.

## Ask the user
- What they want to do (list, view, create, update)
- For creation: describe the trading logic or provide code
