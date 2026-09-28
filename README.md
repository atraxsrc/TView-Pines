# TView Pines

TradingView Pine Script indicators built around the Roman concept.

## Scripts

### Enhanced Roman Order Block
`Enhanced-Roman-Order-Block.pine`

Advanced Order Block indicator with mitigation options, higher timeframe confirmation, size filtering, alerts, and more.

- Bullish & Bearish OB detection
- Wick / Close mitigation toggle
- Minimum OB size filter (ATR based)
- Optional higher timeframe confirmation
- Extend boxes/lines customizable bars
- Max OBs limit + cleanup
- Formation & mitigation alerts

### Roman Trade Setup (H12 to H1)
`Roman-Trade-Setup-H12-H1.pine`

A top-down trade setup: H12 sets the bias, H1 gives the entry trigger.

1. HTF bias via Market Structure Break (12H)
2. 50% fib of the swing that created the bias
3. HTF SFP (only when aligned with bias) plus HTF Order Block / Breaker
4. H1 MSS (single clean label)

Includes zone management (age, distance and height filters), an info table and alerts for HTF bias changes, HTF SFP and H1 MSS. Defaults follow the "Alts" profile; for BTC/ETH try max distance ~5% and max zone height ~2%.

## Usage
1. Open Pine Editor in TradingView
2. Paste the content of the `.pine` file you want
3. Save, then Add to Chart

For the Trade Setup, use a chart timeframe below the HTF (H1 recommended).

## Development
Run `pre-commit run --all-files` before committing.

MIT License
