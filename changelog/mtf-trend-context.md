# MTF Trend Context [Vian] — Changelog

## v1.0.0

### TradingView

- Initial release.
- 5-timeframe trend context.
- Scalping / Intraday / Swing / Custom presets.
- Confirmed-bar state handling for higher, equal, and lower requested timeframes.
- Conservative N/A handling.
- Alignment summary.
- Compact table UI.

### MetaTrader 5 — MQL5 v1.00 port

- Added native MetaTrader 5 custom-indicator port.
- Uses the most recently closed bar (`shift 1`) of each requested timeframe.
- Added `iMA()` handle lifecycle with `BarsCalculated()` readiness checks and `IndicatorRelease()` cleanup.
- Added history synchronization and insufficient-data handling with conservative N/A output.
- Added native compact chart-object panel with Scalping / Intraday / Swing / Custom parity.
- Preserved alignment rules and context-only scope; no trading or signal logic added.
