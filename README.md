# Polymarket Trading Bot (TypeScript) - RSI, MACD, Momentum

A configurable **Polymarket trading bot** for 15m Up/Down markets using RSI, MACD, and Momentum signals.

If you are searching for a **Polymarket Arbitrage bot**, this repo is a signal-based trading bot (not a true cross-market arbitrage engine), but it is a practical base to build arbitrage logic on top of the Polymarket CLOB and Gamma APIs.

## What This Bot Does

- Discovers active ETH/BTC Polymarket markets from Gamma API
- Pulls token prices from CLOB API
- Computes rolling RSI / MACD / Momentum indicators
- Produces `BuyUp` / `BuyDown` / `NoAction` decisions
- Runs in simulation mode with detailed logs
- Supports CLOB authentication and order helper methods for extension

## Current Status

- `--simulation`: fully supported and continuously logs signals/actions
- `--live`: currently starts the same loop as simulation (real order execution is scaffolded but not wired into the main loop yet)

## Keywords (Search Match)

- Polymarket trading bot
- Polymarket bot
- Polymarket Arbitrage bot (base project, not full arbitrage yet)
- Polymarket API bot
- Polymarket CLOB bot

## Strategy Modes

Configure under `trending_index.mode`:

- `rsi`
- `macd`
- `macd_signal`
- `momentum`

Core strategy inputs:

- `threshold`
- `lookback`
- `macd_fast_period`
- `macd_slow_period`
- `macd_signal_period`
- `position_size`

## Requirements

- Node.js `>= 18`
- npm
- Polymarket private key for auth checks

## Quick Start

```bash
npm install
copy config.json.example config.json
```

Edit `config.json`:

- Set `polymarket.private_key`
- Optionally set `api_key`, `api_secret`, `api_passphrase`

Run simulation:

```bash
npm run dev
# or
npm run simulation
```

Run live mode entrypoint:

```bash
npm run live
```

Use a custom config path:

```bash
npx tsx src/main.ts --config path/to/config.json
```

## Config Overview

### `polymarket`

- `gamma_api_url`
- `clob_api_url`
- `private_key`
- `api_key`, `api_secret`, `api_passphrase`
- `proxy_wallet_address`
- `signature_type`

### `trending_index`

- `mode`
- `threshold`
- `lookback`
- `macd_fast_period`
- `macd_slow_period`
- `macd_signal_period`
- `use_macd_sl_filter`

### `trading`

- `check_interval_ms`
- `position_size`
- `profit_threshold`
- `stop_loss_threshold`
- `enable_eth_trading`
- `enable_solana_trading`
- `enable_xrp_trading`
- `trading_start_when_remaining_minutes`

## Project Structure

```text
src/
  main.ts         # app entrypoint, auth check, market discovery, mode selection
  config.ts       # config loading and CLI args
  api.ts          # Polymarket Gamma + CLOB wrapper
  clob.ts         # wallet, CLOB client creation, order helper
  monitor.ts      # market discovery and snapshots
  indicators.ts   # rolling RSI/MACD/Momentum
  strategies.ts   # trading decision engine
  simulation.ts   # simulation loop and logging
  types.ts        # app types
```

## How To Extend Into a Real Arbitrage Bot

To convert this into a stronger **Polymarket Arbitrage bot**, add:

- Cross-market price spread detection (related markets / outcome parity)
- Multi-leg execution with slippage controls
- Position netting and inventory risk checks
- Latency-aware quoting and cancellation logic
- PnL accounting per strategy and market

## Risk Disclaimer

This software is for research/education. Trading prediction markets involves significant risk. Test extensively in simulation before real execution.
