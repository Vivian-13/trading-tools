# MTF Trend Context [Vian] — MetaTrader 5

**Version:** 1.00  
**Platform:** MetaTrader 5 / MQL5 custom indicator  
**Primary benefit:** See multi-timeframe trend alignment at a glance.

MTF Trend Context is a compact market-context panel. It classifies five selected timeframes as Bullish, Bearish, Neutral, or N/A and summarizes whether the selected timeframes are aligned or mixed.

It is not a standalone trading signal and does not place trades.

## Trend logic

Default lengths:

- Fast EMA = 20
- Slow EMA = 50

State per timeframe:

- **Bullish:** `Close > Fast EMA > Slow EMA`
- **Bearish:** `Close < Fast EMA < Slow EMA`
- **Neutral:** every other valid configuration
- **N/A:** data/history is not ready or insufficient for reliable classification

The Slow EMA length must be greater than the Fast EMA length.

## Confirmed closed-bar handling

The MT5 port reads the most recently closed bar of each requested timeframe directly.

For every selected timeframe, the indicator reads:

- close price with `CopyClose(..., start_pos=1, count=1, ...)`;
- Fast EMA with `CopyBuffer(..., start_pos=1, count=1, ...)`;
- Slow EMA with `CopyBuffer(..., start_pos=1, count=1, ...)`.

In MQL5 timeseries/indicator access, position `0` is the current forming bar, so position `1` is the most recently closed bar. This rule is the same whether the requested timeframe is lower than, equal to, or higher than the chart timeframe.

Before classifying a state, the indicator checks history synchronization, available bar count, and `BarsCalculated()` for both EMA handles. If the required data is not ready, it displays `N/A` instead of inferring a state.

## Presets

| Preset | Timeframes |
| --- | --- |
| Scalping | M1, M5, M15, H1, H4 |
| Intraday (default) | M5, M15, H1, H4, D1 |
| Swing | H1, H4, D1, W1, MN1 |
| Custom | User-selected TF1–TF5 using `ENUM_TIMEFRAMES` |

The preset does not change automatically with the chart timeframe.

## Alignment

Strong alignment is shown only when all five timeframe states are valid:

- 5/5 Bullish → `ALL BULLISH (5/5)`
- 4/5 Bullish → `MOSTLY BULLISH (4/5)`
- 5/5 Bearish → `ALL BEARISH (5/5)`
- 4/5 Bearish → `MOSTLY BEARISH (4/5)`
- all other valid combinations → `MIXED`

If any timeframe is `N/A`, the footer remains conservative and reports `MIXED (x/5 data)`.

## UI

The indicator uses a compact native chart-object panel:

- header: `MTF TREND CONTEXT`;
- two columns: `TF` and `STATE`;
- five timeframe rows;
- optional Alignment footer;
- default position: top-right;
- muted steel, green, red, and gray palette.

The object tree is created once during initialization. Normal refreshes update cell text and background colors rather than recreating the panel on every tick.

## Inputs

### Trend

- Fast EMA Length = 20
- Slow EMA Length = 50

### Timeframes

- Preset = Intraday
- Custom TF1
- Custom TF2
- Custom TF3
- Custom TF4
- Custom TF5

### Display

- Panel Corner = Top Right
- Text Size = Medium
- Show Alignment = true

## Usage

1. Compile `MTF_Trend_Context_Vian.mq5` in MetaEditor.
2. Attach it to any MT5 chart.
3. Leave the default Intraday preset or choose Scalping, Swing, or Custom.
4. Read the five states as context, not as entries.
5. Use the Alignment row to see whether the selected timeframes are broadly aligned or mixed.

Recommended verification chart: **M15 + Intraday preset**. This shows M5 below the chart timeframe, M15 equal to it, and H1/H4/D1 above it in one test.

## Limitations

- This is a market-context indicator, not a BUY/SELL system.
- It does not predict future price movement.
- It does not trade or include entries, exits, stops, targets, alerts, backtests, win rate, volume, volatility, market structure, sessions, scanners, or other filters.
- EMA-based classification is intentionally simple and can lag price.
- A broker/terminal may need time to synchronize history for a requested symbol/timeframe; affected rows display `N/A` until required data is available.

## Compile status

**static-reviewed, awaiting MetaEditor compiler verification**

## License

Mozilla Public License 2.0.