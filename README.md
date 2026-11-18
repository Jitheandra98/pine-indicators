# Pine Script Indicators — Gold Trading Systems

14 Pine Script v6 indicators for XAUUSD / gold futures (GC, MGC), selected from 290+ scripts written
and iterated since September 2025. ICT/SMC market-structure concepts: order blocks, fair-value
gaps, liquidity pools and sweeps, market-structure shifts (BOS/CHoCH), premium/discount
positioning, multi-timeframe bias, and session killzones.

> **Results, stated plainly (updated November 2026).** In October 2026 the scripts here, along with
> the rest of the 290+, were run unchanged on 2016–2026 gold data with trading costs and
> out-of-sample stages. None passed; scripts that draw no trade signals could not be tested. This
> repo is a record of the work and the measurement methods, not a trading recommendation.

## Layout

### `quantum-flow/` — the evolution (v18 → v25)
The Quantum Flow line: a full SMC decision engine that grew version by version — bias engines,
zone-reaction scoring, confluence ladders, discipline gates, live win-rate tracking.
Included deliberately **with its flaws**: v19 reached 417 inputs and became a lesson in
over-engineering (see the audit in the companion research repo). v18.1 contains targeted fixes:
chart-relative bias timeframes, conservative intrabar trade resolution, corrected RSI regime labels.

### `systems/` — lean, honestly-measured systems
Small single-thesis indicators with a shared honesty layer:
- **`ob_react_v1.pine`** — order-block reaction system designed from a 25-day replay study
  (Jun–Jul 2026, 315 simulated trades). In that sample, order blocks held more often than FVGs,
  and broken-zone "breaker" re-entries lost money, so breakers are excluded. The sample was short
  and covered one market regime: later tests on 2016–2026 data found zone reactions no better
  than randomly placed control zones. First-touch entries, dead-zone flagging, volatility go-windows.
- **`mtf_cascade_honest_pnl.pine`** — lower→higher timeframe confirmation cascade (1m→3m→5m→15m).
- **`asian_range_break_honest_pnl.pine`** — Asian-range/London-breakout test harness. Verdict from
  its own dashboard: trend beta, not edge — kept as a documented negative result.

Every system reports: cost-inclusive net P&L, stop-first resolution on ambiguous bars,
long/short split, buy-and-hold benchmark, and an explicit **two-sided (STRUCTURE) vs beta verdict**.
A strategy only counts if it is profitable long AND short in the same regime.

## Design principles
1. Conservative measurement beats flattering measurement.
2. An edge must beat buy-and-hold and work both directions — otherwise it's market drift.
3. Fewer inputs beat more inputs (v19's 417 inputs proved the point the hard way).
4. A pattern found in a few weeks of data must survive years of out-of-sample data before it counts.

*Built with AI pair-programming (Claude Code). Chart automation used the open-source
[tradingview-mcp](https://github.com/tradesdontlie/tradingview-mcp) bridge (Chrome DevTools Protocol).*
