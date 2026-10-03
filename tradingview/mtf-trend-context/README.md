# MTF Trend Context [Vian]

**Version:** v1.0.0  
**Platform:** TradingView / Pine Script v6  
**Price:** Free  
**Primary benefit:** See multi-timeframe trend alignment at a glance.

MTF Trend Context is a compact market-context tool. It helps a trader see whether five important timeframes are broadly aligned, mixed, or neutral without adding moving-average plots, entry arrows, or trade signals to the chart.

## What it does

Each selected timeframe is classified using price and two EMAs:

- **Bullish:** `Close > Fast EMA > Slow EMA`
- **Bearish:** `Close < Fast EMA < Slow EMA`
- **Neutral:** every other valid configuration
- **N/A:** insufficient data to classify the timeframe reliably

Defaults are Fast EMA = 20 and Slow EMA = 50. The slow length must be greater than the fast length.

## Presets

The indicator always evaluates five timeframes.

| Preset | Timeframes |
| --- | --- |
| Scalping | 1m, 5m, 15m, 1H, 4H |
| Intraday (default) | 5m, 15m, 1H, 4H, 1D |
| Swing | 1H, 4H, 1D, 1W, 1M |
| Custom | User-selected TF1–TF5 |

Changing the chart timeframe does not automatically change the selected preset.

## Confirmed-bar handling

The tool prioritizes stable, closed-bar context over responsiveness to developing candles.

- **Requested timeframe above the chart timeframe:** uses TradingView's documented higher-timeframe pattern with a one-bar offset and `barmerge.lookahead_on`, so the displayed state comes from the last confirmed requested-timeframe bar.
- **Requested timeframe equal to the chart timeframe:** uses the current chart bar only when it is confirmed; otherwise it uses the previous chart bar.
- **Requested timeframe below the chart timeframe:** uses `request.security_lower_tf()` and selects the most recent intrabar whose close time has passed on a live chart bar. If the current chart bar contains no confirmed lower-timeframe intrabar yet, it falls back to the last confirmed state from the preceding chart bar.

This design avoids using a developing higher-, equal-, or lower-timeframe candle as the displayed state. TradingView notes that lower-timeframe requests can still be revised in rare cases because realtime and historical provider feeds can differ, so the project does not claim absolute immunity from all possible data-feed repainting.

## Alignment

Alignment is only classified as strong when all five timeframe states are available:

- 5/5 Bullish → `ALL BULLISH`
- 4/5 Bullish → `MOSTLY BULLISH`
- 5/5 Bearish → `ALL BEARISH`
- 4/5 Bearish → `MOSTLY BEARISH`
- anything else → `MIXED`

If one or more timeframes are N/A, the footer stays conservative and reports `MIXED · x/5 data`.

## Usage

1. Add the indicator to a standard TradingView chart.
2. Leave the default Intraday preset or select Scalping, Swing, or Custom.
3. Read the five timeframe states as context, not as entries.
4. Use the Alignment footer to see whether the selected timeframes are broadly aligned or mixed.
5. Adjust the EMA lengths only if they fit your own process. Keep the slow EMA longer than the fast EMA.

## Limitations

- This is a context tool, not a BUY/SELL system.
- It does not predict future price movement.
- It does not include alerts, entries, exits, stops, targets, backtests, volume, volatility, market structure, or other filters.
- EMA-based classification is intentionally simple and can lag price.
- Very limited chart or requested-timeframe history can produce N/A.
- Lower-timeframe availability depends on TradingView plan limits and the underlying data feed.

## TradingView

TradingView publication link: **Not published yet.**

After the public TradingView URL exists, replace this placeholder with the final script page.

## License

Mozilla Public License 2.0.
