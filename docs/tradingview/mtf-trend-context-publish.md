# TradingView Publication — MTF Trend Context [Vian]

## Status

Source status: **static-reviewed, awaiting TradingView compiler verification**

The source has been reviewed against the current Pine Script v6 documentation for higher-timeframe requests, lower-timeframe intrabar requests, timeframe strings, dynamic requests, tables, bar states, and public-script publishing rules. A TradingView Pine compiler is not available in this workflow, so the script must still be pasted into TradingView and compiled before public publication.

## Title

**MTF Trend Context [Vian]**

## Opening benefit

**See trend alignment across multiple timeframes at a glance.**

## Short description

MTF Trend Context classifies five selected timeframes as Bullish, Bearish, Neutral, or N/A using price and EMA alignment, then summarizes whether the timeframes are aligned or mixed. It is designed as a compact market-context tool, not a standalone trading signal.

## Full description

See trend alignment across multiple timeframes at a glance.

MTF Trend Context is a compact market-context tool that classifies five selected timeframes as Bullish, Bearish, Neutral, or N/A, then summarizes whether those timeframes are broadly aligned or mixed.

**How it works**

Each timeframe uses the same transparent rule:

- Bullish when Close > Fast EMA > Slow EMA
- Bearish when Close < Fast EMA < Slow EMA
- Neutral in every other valid configuration
- N/A when there is not enough data for a reliable classification

The default EMA lengths are 20 and 50, and both are user-adjustable. The slow EMA must remain longer than the fast EMA.

**Presets**

- Scalping: 1m / 5m / 15m / 1H / 4H
- Intraday (default): 5m / 15m / 1H / 4H / 1D
- Swing: 1H / 4H / 1D / 1W / 1M
- Custom: five user-selected timeframes

The preset does not change automatically when the chart timeframe changes.

**Confirmed-bar philosophy**

The tool prioritizes stable context over reacting to a candle that is still forming. Higher-timeframe states use TradingView's documented confirmed-data request pattern. Equal-timeframe states use the latest confirmed chart bar. Lower-timeframe states use TradingView's intrabar request mechanism and exclude lower-timeframe candles whose scheduled close time has not yet passed on a live chart bar.

This prevents developing candles from being treated as confirmed context. TradingView notes that lower-timeframe data can still be revised in rare cases because realtime and historical provider feeds may differ, so this script does not claim absolute immunity from every possible data-feed revision.

**Alignment**

- 5/5 Bullish: ALL BULLISH
- 4/5 Bullish: MOSTLY BULLISH
- 5/5 Bearish: ALL BEARISH
- 4/5 Bearish: MOSTLY BEARISH
- All other combinations: MIXED

If any timeframe is N/A, the tool does not promote the remaining data into a strong alignment label. The footer stays MIXED and shows how many of the five timeframes have valid data.

**Intended use**

Use the panel to answer a simple context question before deeper analysis: are the timeframes you care about generally pointing the same way, or are they conflicting?

It does not generate entries, exits, stop losses, take profits, alerts, predictions, or backtest results.

**Why this is a separate tool**

The EMA formula itself is intentionally simple. The useful part is the compact five-timeframe workflow: fixed presets plus Custom mode, confirmed-bar handling across higher/equal/lower requested timeframes, conservative N/A treatment, and a restrained chart table that keeps context visible without covering price.

**Limitations**

EMA-based trend classification can lag price and does not measure trend quality, volatility, momentum, market structure, or future returns. Different markets and trading styles may require different EMA lengths. Use this as one context input in your own process, not as a standalone trading decision.

## Category suggestions

TradingView currently allows up to three preset category tags. Select the closest available categories in the publishing UI:

1. Trend Analysis
2. Moving Averages
3. Multi-Timeframe Analysis, if that preset category is available

If the exact labels differ in the current UI, choose the nearest equivalent rather than forcing an unrelated category.

## Custom tag suggestions

`multi-timeframe`, `mtf`, `trend-context`, `ema`, `trend-alignment`

## Screenshot checklist

Primary screenshot:

- Use a **standard candlestick chart**.
- Recommended demonstration: a **15-minute chart with the default Intraday preset**. This naturally shows one requested LTF (5m), one equal TF (15m), and three HTFs (1H/4H/1D) in the same view.
- Keep the symbol, chart timeframe, and script name visible in TradingView's status lines.
- Keep the chart clean: no unrelated indicators, no private scripts, no unnecessary drawings.
- Position the table top-right unless it obscures important price action.
- Capture a readable state mix rather than trying to manufacture a bullish or bearish result.

Optional second screenshot:

- A tighter crop emphasizing the compact table and Alignment row.
- Do not add promotional text, performance claims, profit screenshots, or signal-style annotations.

## Publication checklist

1. Open TradingView Pine Editor and paste `MTF_Trend_Context_Vian.pine`.
2. Save the script as `MTF Trend Context [Vian]`.
3. Compile and add it to the chart.
4. Resolve every compiler error and review any warning before publication.
5. Verify Fast EMA = 20, Slow EMA = 50 and confirm that Slow > Fast validation works.
6. Verify all presets:
   - Scalping: 1m / 5m / 15m / 1H / 4H
   - Intraday: 5m / 15m / 1H / 4H / 1D
   - Swing: 1H / 4H / 1D / 1W / 1M
   - Custom: TF1–TF5 user-defined
7. On a 15m chart with Intraday selected, verify LTF/equal/HTF rows update as expected.
8. Check a live chart and confirm the displayed state does not follow a still-forming requested candle.
9. Check a symbol or timeframe with limited history and confirm N/A is displayed rather than a fabricated trend state.
10. Verify alignment counts:
    - 5 bullish → ALL BULLISH
    - 4 bullish → MOSTLY BULLISH
    - 5 bearish → ALL BEARISH
    - 4 bearish → MOSTLY BEARISH
    - otherwise → MIXED
    - any N/A → MIXED with valid-data count
11. Prepare a clean chart that follows TradingView's publication rules.
12. Recommended workflow: publish a **private draft first**, inspect the page, then create the final public publication.
13. For the public publication choose:
    - Privacy: Public
    - Visibility/source: Open
14. Use the title and full description in this document.
15. Do not add GitHub, social-media, contact, pricing, or promotional links to the TradingView publication description; TradingView's public-script rules prohibit external advertising/references there.
16. Choose up to three relevant preset categories and optional custom tags.
17. Publish only after the source compiles cleanly and the chart screenshot is final.
18. After the public script page exists, copy its URL into:
    - `tradingview/mtf-trend-context/README.md`
    - this document, if desired

## License recommendation

Use **Mozilla Public License 2.0 (MPL-2.0)** for both the Pine source and GitHub repository.

TradingView's current Pine style guide and publishing documentation state that open-source Pine scripts use MPL-2.0 by default unless another license is specified. Keeping MPL-2.0 in the source header and the GitHub `LICENSE` file is therefore the simplest consistent choice for this release.
