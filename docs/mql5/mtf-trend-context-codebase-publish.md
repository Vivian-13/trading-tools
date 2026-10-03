# MQL5 CodeBase Publication — MTF Trend Context [Vian]

## Status

Source status: **static-reviewed, awaiting MetaEditor compiler verification**

Target channel: **MQL5 CodeBase**, not MQL5 Market.

## Publication metadata

**Title**  
MTF Trend Context [Vian]

**Language**  
MQL5

**Account type**  
Any

**Category**  
Indicators

**Version**  
1.00

**Source file**  
`MTF_Trend_Context_Vian.mq5`

## Primary statement

**See multi-timeframe trend alignment at a glance.**

## Short summary

A compact MetaTrader 5 indicator that classifies five selected timeframes as Bullish, Bearish, Neutral, or N/A using price and EMA alignment, then summarizes whether the timeframes are aligned or mixed. This is a market-context indicator, not a standalone trading signal.

## Full description

**See multi-timeframe trend alignment at a glance.**

MTF Trend Context [Vian] is a compact MetaTrader 5 market-context indicator. It shows the directional state of five selected timeframes in one panel and summarizes whether those timeframes are broadly aligned or mixed.

### How it works

Each timeframe uses the same transparent rule:

- **Bullish:** Close > Fast EMA > Slow EMA
- **Bearish:** Close < Fast EMA < Slow EMA
- **Neutral:** every other valid configuration
- **N/A:** required history or indicator data is not ready

The default EMA lengths are 20 and 50. Both are adjustable, and the Slow EMA length must remain greater than the Fast EMA length.

### Confirmed closed-bar behavior

Each row uses the most recently closed bar of its own timeframe. The indicator reads price and both EMA values from shift 1, not from the current forming bar.

This behavior is identical whether a selected timeframe is lower than, equal to, or higher than the chart timeframe.

Before showing a state, the indicator checks history synchronization, available bars, and EMA calculation readiness. If the required data is unavailable, it shows N/A instead of estimating a state.

### Presets

- **Scalping:** M1 / M5 / M15 / H1 / H4
- **Intraday (default):** M5 / M15 / H1 / H4 / D1
- **Swing:** H1 / H4 / D1 / W1 / MN1
- **Custom:** five user-selected MetaTrader timeframes

Changing the chart timeframe does not automatically change the selected preset.

### Alignment

- 5/5 Bullish → ALL BULLISH
- 4/5 Bullish → MOSTLY BULLISH
- 5/5 Bearish → ALL BEARISH
- 4/5 Bearish → MOSTLY BEARISH
- all other combinations → MIXED

If any row is N/A, the indicator does not promote the remaining rows into a strong alignment label. It reports MIXED together with the number of valid timeframes.

### Parameters

**Trend**

- Fast EMA Length — default 20
- Slow EMA Length — default 50

**Timeframes**

- Preset — Intraday by default
- Custom TF1–TF5 — used only when Custom is selected

**Display**

- Panel Corner — Top Right by default
- Text Size — Medium by default
- Show Alignment — true by default

### Intended use

Use the panel as a quick market-context check before deeper analysis: are the timeframes you care about generally pointing in the same direction, or are they conflicting?

This is a market-context indicator, not a standalone trading signal.

### Limitations

- It does not place trades.
- It does not generate BUY/SELL signals, entries, exits, stop losses, take profits, alerts, predictions, or backtest results.
- EMA-based trend classification is intentionally simple and can lag price.
- It does not measure trend quality, volatility, volume, momentum, sessions, market structure, or future returns.
- A terminal/broker may require time to synchronize history for some timeframes. Those rows show N/A until the required data is available.

## Screenshot plan

Prepare at least one image no larger than **750 × 500 px**.

Recommended primary screenshot:

- standard candlestick chart;
- chart timeframe: **M15**;
- preset: **Intraday**;
- panel visible at top-right;
- symbol/timeframe visible in the platform UI;
- no unrelated indicators, trade arrows, private tools, P/L overlays, or promotional text;
- capture a normal readable mix of states rather than manufacturing a bullish or bearish result.

Optional second screenshot:

- closer crop of the panel showing the five rows and Alignment footer;
- keep the image functional rather than promotional.

## Current CodeBase publishing facts

- CodeBase is the MQL4/MQL5 **source-code library** and distributes programs through MQL5.com, MetaTrader and MetaEditor.
- Current CodeBase guidance describes a free source-code submission flow; it does not document a Seller-verification step for CodeBase publishing. Seller verification belongs to the separate Market/commercial flow.
- The indicator submission category is **Indicators** and account type can be **Any** for this indicator.
- Attach the **source `.mq5` file**, not only a compiled `.ex5` file.
- For a single indicator source file, choose **Location = Default**. CodeBase downloads an indicator published this way to `MQL5\Indicators\Downloads\`.
- At least one screenshot is required; current guidance specifies images up to **750 × 500 px**.
- After saving the description/files, submit with **Ready** to the automatic validator.
- If validation succeeds, the **Publish** action becomes available. If validation fails, correct the reported issues and resubmit.

## CodeBase submission checklist

Complete this only after local MetaEditor compilation is clean.

1. Log in to MQL5.com.
2. Open **CodeBase** and choose **Submit your code**.
3. Set:
   - Subject: `MTF Trend Context [Vian]`
   - Language: `MQL5`
   - Account type: `Any`
   - Category: `Indicators`
4. Create the code entry and accept the CodeBase formatting/rules pages shown by the site.
5. Enter the Short summary from this document.
6. Enter the Full description from this document.
7. Attach `MTF_Trend_Context_Vian.mq5` as the source file.
8. Set file Location to **Default**.
9. Attach at least one clean screenshot, maximum 750 × 500 px.
10. Save the draft.
11. Click **Ready** to submit it to the automatic validator.
12. Read the validator report carefully.
13. If there are errors, do not publish; fix the source locally, compile again, update the CodeBase attachment, and rerun validation.
14. When validation succeeds and **Publish** becomes available, review the final page once more and publish.
15. After publication, record the public CodeBase URL in the GitHub README/docs.

## Local pre-submission verification

Before CodeBase submission, verify in MetaTrader 5:

- MetaEditor: 0 errors, 0 meaningful warnings.
- M15 chart + Intraday preset shows M5 / M15 / H1 / H4 / D1.
- Scalping preset shows M1 / M5 / M15 / H1 / H4.
- Swing preset shows H1 / H4 / D1 / W1 / MN1.
- Custom uses all five selected `ENUM_TIMEFRAMES` values.
- Slow EMA <= Fast EMA is rejected as invalid input.
- Missing/not-ready data shows N/A.
- Any N/A prevents ALL/MOSTLY alignment.
- The state does not move with a still-forming H1/H4/D1 candle.
- Panel remains anchored and readable after chart resize.
- Changing chart symbol/timeframe cleanly reinitializes the indicator.
- Removing the indicator removes its panel objects and releases indicator handles.