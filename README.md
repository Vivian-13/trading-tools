# Vian — Systematic Trading Builder

**Building trading tools and systems. Testing ideas with data before trusting them.**

This repository contains public, free trading tools built under the Vian brand. The focus is practical trader-facing utilities with clear logic, restrained interfaces, and honest limitations.

## Repository structure

- `tradingview/` — TradingView / Pine Script tools.
- `mql5/` — MetaTrader 5 / MQL5 public tools and ports.
- `docs/` — Publication notes and user-facing release material.
- `screenshots/` — Guidance and assets for clean public screenshots.
- `changelog/` — Version history for released tools.

## Current release

### MTF Trend Context [Vian] v1.0.0

A compact five-timeframe market-context panel that classifies each selected timeframe as Bullish, Bearish, Neutral, or N/A and summarizes alignment without generating trading signals.

Source and documentation:

**TradingView**
- `tradingview/mtf-trend-context/MTF_Trend_Context_Vian.pine`
- `tradingview/mtf-trend-context/README.md`
- `docs/tradingview/mtf-trend-context-publish.md`

**MetaTrader 5 / MQL5**
- `mql5/mtf-trend-context/MTF_Trend_Context_Vian.mq5`
- `mql5/mtf-trend-context/README.md`
- `docs/mql5/mtf-trend-context-codebase-publish.md`
- MQL5 CodeBase: https://www.mql5.com/en/code/78506

## License

Source code in this repository is released under the Mozilla Public License 2.0 unless a file states otherwise.
