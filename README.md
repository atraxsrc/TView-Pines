
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
4. LTF MSS on the chart timeframe (single clean label), filtered by default by a recent zone tap (or broken-level retest) and/or SFP
Includes zone management (age, distance and height filters), an info table and alerts for HTF bias changes, HTF SFP and LTF MSS. Defaults follow the "Alts" profile; for BTC/ETH try max distance ~5% and max zone height ~2%.
 
**rev 6**
- `LTF MSS also requires` defaults to *Zone tap or SFP*, so "armed" in the table now means a setup is actually in a zone. Charts that saved *None* keep it until you change it.
- Thin order blocks: when the OB candle's body is smaller than `Thin body -> use wick` x HTF ATR(14) (a near doji), the zone uses the full wick range.
- Broken HTF level: the swing the bias break closed through is drawn as a grey retest line. Once price has moved one LTF ATR away, a retest of it counts as a zone tap. After a fast, waterfall break this level is usually much closer than the OB.
- Optional counter-trend mode (off by default): an HTF SFP *against* the bias arms an `MSS CT` in the SFP direction, with its own alerts and table row. Trade it smaller.
- New inputs live in their own group after *Colors*, so existing inputs keep their ids and saved chart settings stay in place.
**rev 7**
- Next HTF MSS levels: dotted lines at the still-intact HTF swing high and low, plus two table rows (*Bullish MSS* / *Bearish MSS*) with the exact HTF close that would trigger the next MSS and its distance from price. The row marked **FLIP** is the one that turns the current bias. "Waiting for a new swing" means no intact swing exists yet, so a new HTF pivot has to confirm first.
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
| Only A+ entries | `LTF MSS also requires` = Zone tap or SFP (default) or stricter: Zone tap, tune `Setup window` |
| More / fewer entry labels | Lower / raise `LTF pivot length` |
| Signals before the HTF candle closes | Turn off `Act only on CLOSED HTF bars` (this repaints) |
| Entries after a fast break | Keep `Retest of broken level counts as a zone tap` on; the grey line is the level |
| Counter-trend trades after a sweep | Turn on `Counter-trend MSS after an opposite HTF SFP`, trade `MSS CT` smaller |
| Zones too thin (doji OBs) | Raise `Thin body -> use wick`, 0 = always use the body |
| Know when the bias will flip | Read the *Bullish / Bearish MSS* table rows (FLIP marks the bias-turning one); toggle the lines with `Show next HTF MSS levels` |
 
Alerts: with closed HTF bars on (default), set the four HTF alerts to "Once Per Bar" so they fire right at the HTF close. Use "Once Per Bar Close" for everything when running in live HTF mode. `LTF MSS up/down` fire on bias-aligned entries only; counter-trend entries have their own `LTF counter-trend MSS up/down` alerts.
 
## Usage
1. Open Pine Editor in TradingView
2. Paste the content of the `.pine` file you want
3. Save, then Add to Chart
For the Trade Setup, use a chart timeframe below the HTF (H1 recommended).
 
## Development
MIT License
 
