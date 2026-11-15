# TView Pines

TradingView Pine Script indicators built around the Roman concept.

## Scripts

### Enhanced Roman Order Block
`Enhanced-Roman-Order-Block.pine`

Advanced Order Block indicator with mitigation options, higher timeframe confirmation, size filtering, alerts, and more.

- Bullish & Bearish OB detection (closed bars only, no intrabar flicker)
- Wick / Close mitigation toggle
- Minimum OB size filter (ATR based)
- Optional higher timeframe confirmation
- Live blocks keep extending with the chart
- Max OBs limit (mitigated blocks are dropped first)
- Formation & mitigation alerts

### Roman Trade Setup (H12 to H1)
`Roman-Trade-Setup-H12-H1.pine`

A top-down trade setup: H12 sets the bias, H1 gives the entry trigger.

1. HTF bias via Market Structure Break (12H)
2. 50% fib of the swing that created the bias
3. HTF SFP (only when aligned with bias) plus HTF Order Block / Breaker
4. LTF MSS on the chart timeframe (single clean label), optionally filtered by a recent zone tap and/or SFP

Includes zone management (age, distance and height filters), an info table and alerts for HTF bias changes, HTF SFP and LTF MSS. Defaults follow the "Alts" profile; for BTC/ETH try max distance ~5% and max zone height ~2%.

## Settings guide

Both scripts can draw this guide on the chart, with your current values in brackets: tick `Show settings guide on chart` in the `Guide` group at the bottom of the Inputs tab.

### Enhanced Roman Order Block

| You want | Change |
| --- | --- |
| Fewer, stronger blocks | Raise `Min OB Size (ATR Multiple)` (0.5 to 1.0+), keep `Lookback Candles` at 3 |
| More blocks | Lower `Min OB Size`, raise `Lookback Candles` (slower displacements also count) |
| Blocks that survive a quick wick | `Mitigation Type` = Close |
| A clean chart | Turn off `Show Mitigated Order Blocks`, lower `Max OBs to Show` |
| Only blocks that swept HTF liquidity | Set `Higher Timeframe for Confirmation` (for example 240 on a 15m chart) |
| Alerts | Tick the alert inputs, then create an alert with "Any alert() function call" |

### Roman Trade Setup

| You want | Change |
| --- | --- |
| BTC / ETH instead of alts | `Max distance from price` ~5, `Max zone height` ~2 |
| Fewer bias flips | Raise `HTF pivot length` (3 to 5) |
| Zones disappear too fast | Raise `Max zone age`, keep `Always keep newest zone` on. Zones past `Max distance` are only hidden and return when price comes back |
| Too many zones | `Max zones per direction` = 1, turn on `Delete opposing zones on bias flip` |
| Only A+ entries | `LTF MSS also requires` = Zone tap or SFP (or stricter: Zone tap), tune `Setup window` |
| More / fewer entry labels | Lower / raise `LTF pivot length` |
| Signals before the HTF candle closes | Turn off `Act only on CLOSED HTF bars` (this repaints) |

Alerts: with closed HTF bars on (default), set the four HTF alerts to "Once Per Bar" so they fire right at the HTF close. Use "Once Per Bar Close" for everything when running in live HTF mode.

## Usage
1. Open Pine Editor in TradingView
2. Paste the content of the `.pine` file you want
3. Save, then Add to Chart

For the Trade Setup, use a chart timeframe below the HTF (H1 recommended).

## Development
MIT License
